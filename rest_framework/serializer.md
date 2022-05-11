**from rest_framework.serializers import ModelSerializer**

定义field_name= serializers.SerializerMethodField()，def get_field(self,obj):pass

定义 validate_field_name(self,value):return True 验证字段

```python
class modelSerializer(ModelSerializer):
    field_name = serializers.SerializerMethodField()
    def get_field(self,obj):pass
    def validate_field_name(self,value):return True
    
```



