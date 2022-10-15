# Uploading Images to Django REST Framework from Forms in React

## settings.py

````
import os

# Actual directory user files go to
MEDIA_ROOT = os.path.join(os.path.dirname(BASE_DIR), 'mediafiles')

# URL used to access the media
MEDIA_URL = '/media/'
````

## urls.py

````
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/users/', include('users.urls')),
    path('api/', include('commerce.urls')),

] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
````

## models.py
````
# lets us explicitly set upload path and filename
def upload_to(instance, filename):
    return 'images/{filename}'.format(filename=filename)

class MyModel(models.Model):
    creator = models.ForeignKey(
        User, on_delete=models.CASCADE, related_name="listings")
    title = models.CharField(
        max_length=80, blank=False, null=False)
    description = models.TextField()
    image_url = models.ImageField(upload_to=upload_to, blank=True, null=True)
````

## views.py

````
from .models import MyModel
from .serializers import MyModelSerializer
from rest_framework import permissions
from rest_framework.parsers import MultiPartParser, FormParser

class MyModelViewSet(viewsets.ModelViewSet):
    queryset = MyModel.objects.order_by('-creation_date')
    serializer_class = MyModelSerializer
    parser_classes = (MultiPartParser, FormParser)
    permission_classes = [
        permissions.IsAuthenticatedOrReadOnly]

    def perform_create(self, serializer):
        serializer.save(creator=self.request.user)
````

## Serializer

````
from rest_framework import serializers
from .models import MyModel

class MyModelSerializer(serializers.ModelSerializer):

    creator = serializers.ReadOnlyField(source='creator.username')
    creator_id = serializers.ReadOnlyField(source='creator.id')
    image_url = serializers.ImageField(required=False)

    class Meta:
        model = MyModel
        fields = ['id', 'creator', 'creator_id', 'title', 'description', 'image_url']
````

# Reactside

````
 <input type="file" 
    name="image_url"
    accept="image/jpeg,image/png,image/gif"
    onChange={(e) => {handleImageChange(e)}}>
````

## CreateMyModelForm.js

````
import React, { useState } from "react";

// React-Bootstrap
import Form from "react-bootstrap/Form";
import Button from "react-bootstrap/Button";
import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";
import API from "../../API";

const CreateMyModel = () => {

    const [data, setData] = useState({
        title: "",
        description: "",
        image_url: "",
    });
    const [errors, setErrors] = useState({
        title: "",
        description: "",
        image_url: "",
    });


    const handleChange = ({ currentTarget: input }) => {
        let newData = { ...data };
        newData[input.name] = input.value;
        setData(newData);
    };

    const handleImageChange = (e) => {
        let newData = { ...data };
        newData["image_url"] = e.target.files[0];
        setData(newData);
    };

    const doSubmit = async (e) => {
        e.preventDefault();
        const response = await API.createMyModelEntry(data);
        if (response.status === 400) {
            setErrors(response.data);
        }
    };

    return (

        <Form>
            <Row>
                <Form.Group className="mb-3" controlId="titleInput">
                    <Form.Label>Title</Form.Label>
                    <Form.Control
                        type="text"
                        name="title"
                        value={data.title}
                        isInvalid={errors.title}
                        onChange={(e) => {
                            handleChange(e);
                        }}
                        maxLength={80}
                    />
                    {errors.title && (
                        <Form.Text className="alert-danger" tooltip>
                            {errors.title}
                        </Form.Text>
                    )}
                </Form.Group>
            </Row>
            <Row>
                <Form.Group controlId="formFile" className="mb-3">
                    <Form.Label>My Image</Form.Label>
                    <Form.Control
                        type="file"
                        name="image_url"
                        accept="image/jpeg,image/png,image/gif"
                        onChange={(e) => {
                            handleImageChange(e);
                        }}
                    />
                    {errors.image_url && (
                        <Form.Text className="alert-danger" tooltip>
                            {errors.image_url}
                        </Form.Text>
                    )}
                </Form.Group>
            </Row>
            <Form.Group className="mb-3" controlId="descriptionInput">
                <Form.Label>Description</Form.Label>
                <Form.Control
                    as="textarea"
                    rows={10}
                    name="description"
                    value={data.description}
                    isInvalid={errors.description}
                    onChange={(e) => {
                        handleChange(e);
                    }}
                />
                {errors.description && (
                    <Form.Text className="alert-danger" tooltip>
                        {errors.description}
                    </Form.Text>
                )}
            </Form.Group>
            <Button
                variant="primary"
                type="submit"
                onClick={(e) => doSubmit(e)}
            </Button>
        </Form>
    );
};

export default CreateMyModel;

````

## snippet from API.js

````
...
createMyModelEntry: async (data) => {
    let form_data = new FormData();
    if (data.image_url)
        form_data.append("image_url", data.image_url, 
        data.image_url.name);
    form_data.append("title", data.title);
    form_data.append("description", data.description);
    form_data.append("category", data.category);

... 
};
````


## API.js

````
import axiosInstance from "./axios";

const apiSettings = {

createListing: async (data) => {
    let form_data = new FormData();
    if (data.image_url)
        form_data.append("image_url", data.image_url, data.image_url.name);
    form_data.append("title", data.title);
    form_data.append("description", data.description);
    form_data.append("category", data.category);
    form_data.append("start_bid", data.start_bid);
    form_data.append("is_active", true);

const myNewModel = await axiosInstance
        .post(`mymodels/`, form_data, {
            headers: {
                "Content-Type": "multipart/form-data",
            },
        }).then((res) => {
            return res;
        }).catch((error) => {
            return error.response;
        });

    if (myNewModel.status === 201) {
        window.location.href = `/mymodels/${myNewModel.data.id}`;
    }
    return myNewModel;
    },
};

export default apiSettings;
````


## CreateMyModelForm.js doSubmit() function

````
...
const doSubmit = async (e) => {
    e.preventDefault();
    const response = await API.createMyModelEntry(data);
    if (response.status === 400) {
        setErrors(response.data);
    }
};
...
````

## console.log(errors)

````
{
    "title": [
        "This field is required."
    ],
    "description": [
        "This field is required."
    ],
    "image_url": [
        "Upload a valid image. The file you uploaded was either not an image or a corrupted image."
    ]
}
````

## CreateMyModelForm.js Title input field

````
...
<Form.Group className="mb-3" controlId="titleInput">
    <Form.Label>Title</Form.Label>
    <Form.Control
        type="text"
        name="title"
        value={data.title}
        isInvalid={errors.title}
        onChange={(e) => { handleChange(e);}}
        maxLength={80}
        />
     {errors.title && (
         <Form.Text className="alert-danger" tooltip>
             {errors.title}
         </Form.Text>
     )}
</Form.Group>
...
````


https://dev.to/thomz/uploading-images-to-django-rest-framework-from-forms-in-react-3jhj





