 
## JS 与 Android原生APP交互 ##


### 1. Custom URI scheme ###

Custom URI语法

    scheme://host/path?key=value

 JS调用

    hoorang://jsopenapp?param=Custom URI scheme
   
java解析

    Uri uri = Uri.parse(url)
    
JS启动APP防攻击，JAVA安全启动方法

    // convert intent scheme URL to intent object  
    Intent intent = Intent.parseUri(uri);  
    // forbid launching activities without BROWSABLE category  
    intent.addCategory("android.intent.category.BROWSABLE");  
    // forbid explicit call  
    intent.setComponent(null);  
    // forbid intent with selector intent  
    intent.setSelector(null);  
    // start the activity by the intent  
    context.startActivityIfNeeded(intent, -1);  
    
    
### 2. Intent-based URI ###
Intent-based URI语法

    intent://host#Intent;parameters;end

JS调用

    hoorang://jsopenapp#Intent;action=android.intent.action.VIEW;category=android.intent.category.DEFAULT;category=android.intent.category.BROWSABLE;S.param=Intent-based URI;end
    
JAVA参数获取

    Intent dataStringIntent = Intent.parseUri(intent.getDataString() , 0);
    if(dataStringIntent.hasExtra("param")){
           message.append("param#" + dataStringIntent.getStringExtra("param"));
    }

JS调用系统APP示例

	window.location = 'intent:smsto:10000#Intent;action=android.intent.action.SENDTO;end';