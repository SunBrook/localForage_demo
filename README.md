# localForage_demo
localForage 案例



> LocalForage：https://localforage.docschina.org/



```javascript
<script src="js/localforage.min.js"></script>

<script type="text/javascript">
   
    window.onload = function () {
        read("types", (value) => {
            console.log(value);
        });

        add("types",[1,2,3,4,5],(value)=>{
            console.log(value);
        });

        remove("types", () => {
            console.log('删除');
        });

        clear(()=>{
            console.log("清空");
        })
    }


    //初始化驱动
    const store = localforage.createInstance({
        name: "MyDbName", //数据库名称
        storeName: 'sn', //数据仓库名称  不同账号对应不同的库
        driver: [
            localforage.WEBSQL,
            localforage.INDEXEDDB,
            localforage.LOCALSTORAGE
        ],  //驱动优先级
        description: 'LocalForage Desc' //描述
    });

    //读取
    function read(key, callback) {
        store.getItem(key, function (err, value) {
            callback(value);
        });
    }

    //设置
    function add(key, value, callback) {
        store.setItem(key, value).then(function (value) {
            callback(value);
        }).catch(function (err) {
            console.log(err);
        });
    }

    //删除Key
    function remove(key, callback) {
        store.removeItem(key).then(function () {
            callback();
        }).catch(function (err) {
            console.log(err);
        })
    }

    //清空数据库
    function clear(callback) {
        localforage.clear().then(function () {
            callback();
        }).catch(function (err) {
            console.log(err);
        })
    }
</script>
```

