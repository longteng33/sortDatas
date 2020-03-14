# sortDatas
数据归类函数  
需求：  
现有一组数据，数据结构为：   
[{id:1,name:"xiaoming",sex:2},{id:2,name:"bytr",sex:1},{id:3,name:"try",sex:1}]  
数据中的每个对象结构相同，要求按对象中的某属性归类，比如按sex归类  
2、归类的要求一般是一个数组，其结构为：  
var sex=[{id:1,field:'女'},{id:2,field:'男'}]  

```
 var cache={};
        sex.forEach(function(sex){
            var _id=sex.id;
           
            cache[_id]=[];
            persons.forEach(function(person){
                var _sex=person.sex;
                if(_sex==_id){
                    cache[_id].push(person);
                }
            })
        })
```

数据归类函数封装  
```
fields,数组，以什么归类  
datas，数组，被归类的数据  

 function sortDatas(fields,datas){
            var cache={};
            //mapping_field,归类项，数据中每个对象中的某个属性名，以它归类，如sex
            //sortType两种匹配类型，单个或多个
            return function(mapping_field,sortType){
                if(sortType!=="single"&&sortType!=="multi"){
                    throw new Error("Invalid sorType,only 'single' or 'multi' is valid value");
                    return;
                }
                fields.forEach(function(field){
                    var _id=field.id;
                    cache[_id]=[];
                    datas.forEach(function(ele){
                        var mapping_val=ele[mapping_field];
                        if(sortType=="single"){
                            if(mapping_val==_id){
                                cache[_id].push(ele);
                            }
                        }else if(sortType=="multi"){
                            if(mapping_val.indexOf(_id)!=-1){
                                cache[_id].push(ele);
                            }
                        }
                    })
                })
                return cache;
            }
        }
```
使用:  
```
var sex_sort=sortDatas(sex,persons);  
sex_sort("sex","single")  
```
