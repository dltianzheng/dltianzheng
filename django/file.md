```python
from StringIO import StringIO
from django.core.files.uploadedfile import TemporaryUploadedFile
from django.core.files.base import ContentFile
from django.core.files import File
def save_file(file_name,content):
    file = ContentFile(name=file_name,content=content)
    data = {
        "file": file
    }
    
    serializer = FileSerializer(data=data)
    serializer.is_valid(raise_exception=True)
    serializer.save()
    instance = serializer.instance
    return instance
```

djagno中保存文件