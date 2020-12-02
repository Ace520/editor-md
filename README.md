# Markdown 编辑器

https://github.com/pandao/editor.md

## iframe使用

``` 

<iframe class="editormd" id="editormd" src="index.html" frameborder="no" border="0" marginwidth="0" marginheight="0"
  scrolling="no" allowtransparency="yes"></iframe>
```

* JS设置内容、获取MD内容、获取html获取内容、监听内容变化、初始化完成事件

``` 

<script>
    var edIframeWin = document.getElementById("editormd").contentWindow;
    setTimeout(function () {
        //设置内容
        edIframeWin.postMessage({
            method: 'setMarkdown',
            content: '## Markdown 编辑器'
        }, "*");
        //获取MD内容
        edIframeWin.postMessage({
            method: 'getMarkdown'
        }, "*");
        //获取html内容
        edIframeWin.postMessage({
            method: 'getHTML'
        }, "*");

        //监听子页面返回
        window.addEventListener("message", function (event) {
            let data = event.data;
            switch (data.method) {
                case 'setMarkdown': //设置内容返回
                    console.log(data.content);
                    break;
                case 'getMarkdown': //获取md内容返回
                    console.log(data.content);
                    break;
                case 'getHTML': //获取html内容返回
                    console.log(data.content);
                    break;
                case 'onload': //初始化完成
                    console.log(data.content);
                    break;
                case 'onchange': //内容改变事件
                    console.log(data.content);
                    break;
            }
        }, false);
    }, 100);
</script>
```
