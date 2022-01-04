# django-lambda


### IAM 생성 후 profile 설정

```shell
$ aws configure
```

### 관련 패키지 설치

```shell
$ pip install django zappa django-s3-storage
```


### settings.py 임시 설정
```python
DATABASES = {}  # serverless 환경에서 sqlite는 사용 불가능

ALLOWED_HOSTS = ["*"]

# css not found issue
S3_BUCKET_NAME = "my-bucket-name"
STATICFILES_STORAGE = "django_s3_storage.storage.StaticS3Storage"

AWS_S3_BUCKET_NAME_STATIC = S3_BUCKET_NAME
AWS_S3_CUSTOM_DOMAIN = f"{S3_BUCKET_NAME}.s3.amazonaws.com"

STATIC_URL = f"https://{AWS_S3_CUSTOM_DOMAIN}/" 

```

### Deploy
```shell
$ python manage.py collectstatic --noinput

$ zappa init

$ zappa deploy dev

$ zappa update dev
```


### To do
- [ ] Database Settings


### References
- https://auth0.com/blog/deploying-django-restful-apis-as-serverless-applications-with-zappa/#Deploying-with-Zappa
