Petición de S3:

`https://bucket-for-testing-calteks.s3.us-east-1.amazonaws.com/1f8d8b24-1e6a-42bc-8ed5-8a1022e87f1c/18df3db7-99a1-418c-bd4d-cab5c509f4b6/a579a284-e752-44a2-ad4a-b0ce5c9cf108/pole_329e15617736443dba24a2c78c7922d2.jpg`

Configuración de CORS en AWS S3 

```json
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
        "GET",
        "HEAD",
        "PUT",
        "POST",
        "DELETE"
    ],
    "AllowedOrigins": [
        "*"
    ],
    "ExposeHeaders": [
    ],
    "MaxAgeSeconds": 3000
    }
]
```

Error en el navegador:

```text
Access to fetch at
https://bucket-for-testing-calteks.s3.us-east-1.amazonaws.
from origin • // localhost : 3801 • has been blocked by
Allow-Origin• header is present on the requested resource.
e > GET
https : / / bucket- for- test ing- calteks. s3. us -east -1. amazonaws .
net: :ERR FAILED
O > TypeError: Failed to fetch
( index)-zl
CORS policy: No 'Access -Control-
CustomCanvasDia10g . vue: 525 @
com/1f8d8b24-1e6a.-a284-e752-44a2-ad4-.
CustomCanvasDia10g. vue : 530
at
at
at
at
at
storeImageData (CustomCanvasDia10g. vue : 525:1)
loadCanvasImg (CustomCanvasDia10g. vue:497 : 1)
async generateCanvas (CustomCanvasDia10g. vue: 540: 1)
async reloadImageRetrieva1 (CustomCanvasDia10g. vue: 545: 1)
async CustomCanvasDia10g. vue: 574:1
```

Qué podría ser? 

Estoy pensando en hacer un presign desde el backend de la aplicación para así pasarlo al frontend. 


Login

- Salt → es distinto. 
- < hhH