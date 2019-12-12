<h2 id="item-1">下载地址、API和DOM地址（英语好的小伙伴可以看看）</h2>
<p>下载地址：<a href="https://github.com/kartik-v/bootstrap-fileinput" rel="nofollow noreferrer">https://github.com/kartik-v/b...</a><br>API文档 ：<a href="http://plugins.krajee.com/file-input" rel="nofollow noreferrer">http://plugins.krajee.com/fil...</a><br>D E M O：<a href="http://plugins.krajee.com/file-input/demo" rel="nofollow noreferrer">http://plugins.krajee.com/fil...</a></p>
<hr>
<p>做项目用到bootstrap fileinput插件上传文件，在用的过程中，遇到一些问题，所以想着整理一份比较详细的文档，方便自己今后使用，也希望能给大家带来帮助，如有错误，希望大家积极指正，积极交流。<br><strong>注意：第三部分内容因为存在i标签，某些文字被转换成图标</strong></p>
<h3 id="item-1-1">一、引入文件</h3>
<p>&lt;link href="../css/bootstrap.min.css"rel="stylesheet"&gt;<br>&lt;link href="../css/fileinput.css" media="all"rel="stylesheet" type="text/css" /&gt;<br>&lt;scriptsrc="../js/jquery-2.0.3.min.js"&gt;&lt;/script&gt;<br>&lt;script src="../js/fileinput.js"type="text/javascript"&gt;&lt;/script&gt;<br>&lt;script src="../js/bootstrap.min.js"type="text/javascript"&gt;&lt;/script&gt;</p>
<h3 id="item-1-2">二、初始化设置</h3>
<pre class="hljs javascript"><code><span class="hljs-comment">//初始化fileinput</span>
initFileInput();
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">initFileInput</span>(<span class="hljs-params"></span>) </span>{
    $(<span class="hljs-string">"#uploadImg"</span>).fileinput({
        <span class="hljs-attr">language</span>: <span class="hljs-string">'zh'</span>, <span class="hljs-comment">//设置语言</span>
        dropZoneTitle: <span class="hljs-string">'可以将图片拖放到这里 …支持多文件上传'</span>,
        <span class="hljs-attr">uploadUrl</span>: <span class="hljs-string">"index.php"</span>, <span class="hljs-comment">//上传的地址</span>
        uploadExtraData: <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">previewId, index</span>) </span>{   <span class="hljs-comment">//该插件可以向您的服务器方法发送附加数据。这可以通过uploadExtraData在键值对中设置为关联数组对象来完成。所以如果你有设置uploadExtraData={id:'kv-1'}，在PHP中你可以读取这些数据$_POST['id']</span>
            <span class="hljs-keyword">var</span> id = $(<span class="hljs-string">'#id'</span>).val();
            <span class="hljs-keyword">return</span> {<span class="hljs-attr">seriesId</span>: id};
        },
        <span class="hljs-attr">allowedFileExtensions</span>: [<span class="hljs-string">'jpg'</span>,<span class="hljs-string">'png'</span>],<span class="hljs-comment">//接收的文件后缀</span>
        uploadAsync: <span class="hljs-literal">true</span>, <span class="hljs-comment">//默认异步上传</span>
        showUpload: <span class="hljs-literal">true</span>, <span class="hljs-comment">//是否显示上传按钮</span>
        showRemove: <span class="hljs-literal">true</span>, <span class="hljs-comment">//显示移除按钮</span>
        showPreview: <span class="hljs-literal">true</span>, <span class="hljs-comment">//是否显示预览</span>
        showCancel:<span class="hljs-literal">true</span>,   <span class="hljs-comment">//是否显示文件上传取消按钮。默认为true。只有在AJAX上传过程中，才会启用和显示</span>
        showCaption: <span class="hljs-literal">true</span>,<span class="hljs-comment">//是否显示文件标题，默认为true</span>
        browseClass: <span class="hljs-string">"btn btn-primary"</span>, <span class="hljs-comment">//文件选择器/浏览按钮的CSS类。默认为btn btn-primary</span>
        dropZoneEnabled: <span class="hljs-literal">true</span>,<span class="hljs-comment">//是否显示拖拽区域</span>
        minImageWidth: <span class="hljs-number">50</span>, <span class="hljs-comment">//图片的最小宽度</span>
        minImageHeight: <span class="hljs-number">50</span>,<span class="hljs-comment">//图片的最小高度</span>
        maxImageWidth: <span class="hljs-number">1000</span>,<span class="hljs-comment">//图片的最大宽度</span>
        maxImageHeight: <span class="hljs-number">1000</span>,<span class="hljs-comment">//图片的最大高度</span>
        maxFileSize: <span class="hljs-number">1024</span>,<span class="hljs-comment">//单位为kb，如果为0表示不限制文件大小</span>
        minFileCount: <span class="hljs-number">1</span>, <span class="hljs-comment">//每次上传允许的最少文件数。如果设置为0，则表示文件数是可选的。默认为0</span>
        maxFileCount: <span class="hljs-number">0</span>, <span class="hljs-comment">//每次上传允许的最大文件数。如果设置为0，则表示允许的文件数是无限制的。默认为0</span>
        previewFileIcon: <span class="hljs-string">"&lt;i class='glyphicon glyphicon-king'&gt;&lt;/i&gt;"</span>,<span class="hljs-comment">//当检测到用于预览的不可读文件类型时，将在每个预览文件缩略图中显示的图标。默认为&lt;i class="glyphicon glyphicon-file"&gt;&lt;/i&gt;  </span>
        layoutTemplates:{
            <span class="hljs-attr">actionUpload</span>:<span class="hljs-string">''</span><span class="hljs-comment">//去除上传预览缩略图中的上传图片</span>
            actionZoom:<span class="hljs-string">''</span>,   <span class="hljs-comment">//去除上传预览缩略图中的查看详情预览的缩略图标</span>
            actionDownload:<span class="hljs-string">''</span> <span class="hljs-comment">//去除上传预览缩略图中的下载图标</span>
            actionDelete:<span class="hljs-string">''</span>, <span class="hljs-comment">//去除上传预览的缩略图中的删除图标</span>
        },<span class="hljs-comment">//对象用于渲染布局的每个部分的模板配置。您可以设置以下模板来控制窗口小部件布局.eg:去除上传图标</span>
        msgFilesTooMany: <span class="hljs-string">"选择上传的文件数量({n}) 超过允许的最大数值{m}！"</span>,<span class="hljs-comment">//字符串，当文件数超过设置的最大计数时显示的消息 maxFileCount。默认为：选择上传的文件数（{n}）超出了允许的最大限制{m}。请重试您的上传！</span>
    }).on(<span class="hljs-string">'filebatchpreupload'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event, data</span>) </span>{ <span class="hljs-comment">//该方法将在上传之前触发</span>
        <span class="hljs-keyword">var</span> id = $(<span class="hljs-string">'#id option:selected'</span>).val();
        <span class="hljs-keyword">if</span>(id == <span class="hljs-number">0</span>){
            <span class="hljs-keyword">return</span> {
                <span class="hljs-attr">message</span>: <span class="hljs-string">"请选择"</span>, <span class="hljs-comment">// 验证错误信息在上传前要显示。如果设置了这个设置，插件会在调用时自动中止上传，并将其显示为错误消息。您可以使用此属性来读取文件并执行自己的自定义验证</span>
                data:{} <span class="hljs-comment">// any other data to send that can be referred in `filecustomerror`</span>
            };
        }
    });
}
<span class="hljs-comment">//fileuploaded此事件仅针对ajax上传触发，并在每个缩略图文件上传完成后触发。此事件仅针对ajax上传并在以下情况下触发：当点击每个预览缩略图中的上传图标并且文件上传成功时，或者当你有 uploadAsync设置为true您已触发批量上传。在这种情况下，fileuploaded每一个人选择的文件被上传成功后，触发事件。</span>
<span class="hljs-keyword">var</span> id_str = <span class="hljs-string">''</span>;
$(<span class="hljs-string">'#uploadImg'</span>).on(<span class="hljs-string">'fileuploaded'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">event, data, previewId, index</span>) </span>{
    <span class="hljs-keyword">if</span>(<span class="hljs-keyword">typeof</span>(data.response.id) != <span class="hljs-string">'undefined'</span>){
        id_str = id_str+data.response.id+<span class="hljs-string">','</span>;
    }
});
<span class="hljs-comment">// filebatchuploadcomplete此事件仅在ajax上传和完成同步或异步ajax批量上传后触发。</span>
$(<span class="hljs-string">'#uploadImg'</span>).on(<span class="hljs-string">'filebatchuploadcomplete'</span>,<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">event,files,extra</span>) </span>{
    <span class="hljs-keyword">if</span>(id_str.length == <span class="hljs-number">0</span>){
        layer.msg(<span class="hljs-string">'上传失败'</span>, {<span class="hljs-attr">icon</span>: <span class="hljs-number">0</span>});<span class="hljs-comment">//弹框提示</span>
        <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>;
    }
    setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>)</span>{ <span class="hljs-comment">//执行延时关闭</span>
        closeSelf();
    },<span class="hljs-number">1000</span>);
});</code></pre>
<h3 id="item-1-3">三、Options 说明</h3>
<table>
<thead><tr>
<th align="left">属性名</th>
<th align="left">属性类型</th>
<th align="left">描述说明</th>
<th align="left">默认值</th>
</tr></thead>
<tbody>
<tr>
<td align="left">language</td>
<td align="left">String</td>
<td align="left">多语言设置，使用时需提前引入locales文件夹下对应的语言文件，中文zh，引入语言文件必须放在fileinput.js之后</td>
<td align="left">'en'</td>
</tr>
<tr>
<td align="left">showCaption</td>
<td align="left">Boolean</td>
<td align="left">是否显示被选文件的简介</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">showBrowse</td>
<td align="left">Boolean</td>
<td align="left">是否显示浏览按钮</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">showPreview</td>
<td align="left">Boolean</td>
<td align="left">是否显示预览区域</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">showRemove</td>
<td align="left">Boolean</td>
<td align="left">是否显示移除按钮</td>
<td align="left">true,</td>
</tr>
<tr>
<td align="left">showUpload</td>
<td align="left">Boolean</td>
<td align="left">是否显示上传按钮</td>
<td align="left">true,</td>
</tr>
<tr>
<td align="left">showCancel</td>
<td align="left">Boolean</td>
<td align="left">是否显示取消按钮</td>
<td align="left">true,</td>
</tr>
<tr>
<td align="left">showClose:</td>
<td align="left">Boolean</td>
<td align="left">是否显示关闭按钮</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">showUploadedThumbs</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">browseOnZoneClick</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">autoReplace</td>
<td align="left">Boolean</td>
<td align="left">是否自动替换当前图片，设置为true时，再次选择文件， 会将当前的文件替换掉。</td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">generateFileId</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">previewClass</td>
<td align="left">String</td>
<td align="left">添加预览按钮的类属性</td>
<td align="left">‘’</td>
</tr>
<tr>
<td align="left">captionClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">‘’</td>
</tr>
<tr>
<td align="left">frameClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'krajee-default'</td>
</tr>
<tr>
<td align="left">mainClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'file-caption-main'</td>
</tr>
<tr>
<td align="left">mainTemplate</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">purifyHtml</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">fileSizeGetter</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">initialCaption</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">initialPreview</td>
<td align="left">Array/Object</td>
<td align="left"> </td>
<td align="left">[]</td>
</tr>
<tr>
<td align="left">initialPreviewDelimiter</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'<em>$$</em>'</td>
</tr>
<tr>
<td align="left">initialPreviewAsData</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">initialPreviewFileType</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'image'</td>
</tr>
<tr>
<td align="left">initialPreviewConfig</td>
<td align="left">Array/Object</td>
<td align="left"> </td>
<td align="left">[]</td>
</tr>
<tr>
<td align="left">initialPreviewThumbTags</td>
<td align="left">Array/Object</td>
<td align="left"> </td>
<td align="left">[]</td>
</tr>
<tr>
<td align="left">previewThumbTags</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">initialPreviewShowDelete</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">removeFromPreviewOnError</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">deleteUrl</td>
<td align="left">String</td>
<td align="left">删除图片时的请求路径</td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">deleteExtraData</td>
<td align="left">Object</td>
<td align="left">删除图片时额外传入的参数</td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">overwriteInitial</td>
<td align="left">Boolean</td>
<td align="left"> </td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">previewZoomButtonIcons</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{prev: '',next: '',toggleheader: '',fullscreen: '',borderless: '',close: ''},</td>
</tr>
<tr>
<td align="left">previewZoomButtonClasses</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{prev: 'btn btn-navigate',next: 'btn btn-navigate',toggleheader: 'btn btn-default btn-header-toggle',fullscreen: 'btn btn-default',borderless: 'btn btn-default',close: 'btn btn-default'},</td>
</tr>
<tr>
<td align="left">preferIconicPreview</td>
<td align="left">Boolrean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">preferIconicZoomPreview</td>
<td align="left">Boolrean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">allowedPreviewTypes</td>
<td align="left">undefined</td>
<td align="left"> </td>
<td align="left">undefined</td>
</tr>
<tr>
<td align="left">allowedPreviewMimeTypes</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">allowedFileTypes</td>
<td align="left">Object</td>
<td align="left">接收的文件后缀，如['jpg', 'gif', 'png'],不填将不限制上传文件后缀类型</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">allowedFileExtensions</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">defaultPreviewContent</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">customLayoutTags</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">customPreviewTags</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">previewFileIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">previewFileIconClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'file-other-icon'</td>
</tr>
<tr>
<td align="left">previewFileIconSettings</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">previewFileExtSettings</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">buttonLabelClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'hidden-xs'</td>
</tr>
<tr>
<td align="left">browseIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'&nbsp;'</td>
</tr>
<tr>
<td align="left">browseClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'btn btn-primary'</td>
</tr>
<tr>
<td align="left">removeIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">removeClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'btn btn-default'</td>
</tr>
<tr>
<td align="left">cancelIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">cancelClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'btn btn-default'</td>
</tr>
<tr>
<td align="left">uploadIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">uploadClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'btn btn-default'</td>
</tr>
<tr>
<td align="left">uploadUrl</td>
<td align="left">String</td>
<td align="left">上传文件路径</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">uploadAsync</td>
<td align="left">boolean</td>
<td align="left">是否为异步上传</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">uploadExtraData</td>
<td align="left"> </td>
<td align="left">上传文件时额外传递的参数设置</td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">zoomModalHeight</td>
<td align="left">number</td>
<td align="left"> </td>
<td align="left">480</td>
</tr>
<tr>
<td align="left">minImageWidth</td>
<td align="left">String</td>
<td align="left">图片的最小宽度</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">minImageHeight</td>
<td align="left">String</td>
<td align="left">图片的最小高度</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">maxImageWidth</td>
<td align="left">String</td>
<td align="left">图片的最大宽度</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">maxImageHeight</td>
<td align="left">String</td>
<td align="left">图片的最大高度</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">resizeImage</td>
<td align="left">boolean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">resizePreference</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'width'</td>
</tr>
<tr>
<td align="left">resizeQuality</td>
<td align="left">number</td>
<td align="left"> </td>
<td align="left">0.92</td>
</tr>
<tr>
<td align="left">resizeDefaultImageType</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'image/jpeg'</td>
</tr>
<tr>
<td align="left">minFileSize</td>
<td align="left">number</td>
<td align="left">单位为kb，上传文件的最小大小值</td>
<td align="left">0</td>
</tr>
<tr>
<td align="left">maxFileSize</td>
<td align="left">number</td>
<td align="left">单位为kb，如果为0表示不限制文件大小</td>
<td align="left">0</td>
</tr>
<tr>
<td align="left">resizeDefaultImageType</td>
<td align="left">number</td>
<td align="left"> </td>
<td align="left">25600(25MB)</td>
</tr>
<tr>
<td align="left">minFileCount</td>
<td align="left">number</td>
<td align="left">表示同时最小上传的文件个数</td>
<td align="left">0</td>
</tr>
<tr>
<td align="left">maxFileCount</td>
<td align="left">number</td>
<td align="left">表示允许同时上传的最大文件个数</td>
<td align="left">0</td>
</tr>
<tr>
<td align="left">validateInitialCount</td>
<td align="left">boolean</td>
<td align="left"> </td>
<td align="left">false</td>
</tr>
<tr>
<td align="left">msgValidationErrorClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'text-danger'</td>
</tr>
<tr>
<td align="left">msgValidationErrorIcon</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">' '</td>
</tr>
<tr>
<td align="left">msgErrorClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'file-error-message'</td>
</tr>
<tr>
<td align="left">progressThumbClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">"progress-bar progress-bar-success progress-bar-striped active"</td>
</tr>
<tr>
<td align="left">rogressClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">"progress-bar progress-bar-success progress-bar-striped active"</td>
</tr>
<tr>
<td align="left">progressCompleteClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">"progress-bar progress-bar-success"</td>
</tr>
<tr>
<td align="left">progressErrorClass</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">"progress-bar progress-bar-danger"</td>
</tr>
<tr>
<td align="left">progressUploadThreshold</td>
<td align="left">number</td>
<td align="left"> </td>
<td align="left">99</td>
</tr>
<tr>
<td align="left">previewFileType</td>
<td align="left">String</td>
<td align="left">预览文件类型,内置['image', 'html', 'text', 'video', 'audio', 'flash', 'object',‘other‘]等格式</td>
<td align="left">'image'</td>
</tr>
<tr>
<td align="left">elCaptionContainer</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">elCaptionText</td>
<td align="left">String</td>
<td align="left">设置标题栏提示信息</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">elPreviewContainer</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">elPreviewImage</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">elPreviewStatus</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">elErrorContainer</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">errorCloseButton</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">'&lt;span class="close kv-error-close"&gt;×&lt;/span&gt;'</td>
</tr>
<tr>
<td align="left">slugCallback</td>
<td align="left">function</td>
<td align="left">选择后未上传前 回调方法</td>
<td align="left">null</td>
</tr>
<tr>
<td align="left">dropZoneEnabled</td>
<td align="left">boolean</td>
<td align="left">是否显示拖拽区域</td>
<td align="left">true</td>
</tr>
<tr>
<td align="left">dropZoneTitleClass</td>
<td align="left">String</td>
<td align="left">拖拽区域类属性设置</td>
<td align="left">'file-drop-zone-title'</td>
</tr>
<tr>
<td align="left">fileActionSettings</td>
<td align="left">Object</td>
<td align="left">设置预览图片的显示样式</td>
<td align="left">{showRemove: true,showUpload: false,showZoom: true,showDrag: true,removeIcon: '',removeClass: 'btn btn-xs btn-default',removeTitle: 'Remove file',uploadIcon: '',uploadClass: 'btn btn-xs btn-default',uploadTitle: 'Upload file',zoomIcon: '',zoomClass: 'btn btn-xs btn-default',zoomTitle: 'View Details',dragIcon: '',dragClass: 'text-info',dragTitle: 'Move / Rearrange',dragSettings: {},indicatorNew: '',indicatorSuccess: '',indicatorError: '',indicatorLoading: '',indicatorNewTitle: 'Not uploaded yet',indicatorSuccessTitle: 'Uploaded',indicatorErrorTitle: 'Upload Error',indicatorLoadingTitle: 'Uploading ...'}</td>
</tr>
<tr>
<td align="left">otherActionButtons</td>
<td align="left">String</td>
<td align="left"> </td>
<td align="left">''</td>
</tr>
<tr>
<td align="left">textEncoding</td>
<td align="left">String</td>
<td align="left">编码设置</td>
<td align="left">'UTF-8'</td>
</tr>
<tr>
<td align="left">ajaxSettings</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">ajaxDeleteSettings</td>
<td align="left">Object</td>
<td align="left"> </td>
<td align="left">{}</td>
</tr>
<tr>
<td align="left">showAjaxErrorDetails</td>
<td align="left">boolean</td>
<td align="left"> </td>
<td align="left">true</td>
</tr>
</tbody>
</table>
<h3 id="item-1-4">四、提示说明设置</h3>
<table>
<thead><tr>
<th align="left">属性名</th>
<th align="left">默认值</th>
<th align="left">中文</th>
</tr></thead>
<tbody>
<tr>
<td align="left">fileSingle</td>
<td align="left">file</td>
<td align="left">文件</td>
</tr>
<tr>
<td align="left">filePlural</td>
<td align="left">files</td>
<td align="left">个文件</td>
</tr>
<tr>
<td align="left">browseLabel</td>
<td align="left">Browse &amp;hellip</td>
<td align="left">选择 …</td>
</tr>
<tr>
<td align="left">removeLabel</td>
<td align="left">Remove</td>
<td align="left">移除</td>
</tr>
<tr>
<td align="left">removeTitle</td>
<td align="left">Clear selected files</td>
<td align="left">清除选中文件</td>
</tr>
<tr>
<td align="left">cancelLabel</td>
<td align="left">Cancel</td>
<td align="left">取消</td>
</tr>
<tr>
<td align="left">cancelTitle</td>
<td align="left">Abort ongoing upload</td>
<td align="left">取消进行中的上传</td>
</tr>
<tr>
<td align="left">uploadLabel</td>
<td align="left">Upload</td>
<td align="left">上传</td>
</tr>
<tr>
<td align="left">uploadTitle</td>
<td align="left">Upload selected files</td>
<td align="left">上传选中文件</td>
</tr>
<tr>
<td align="left">msgNo</td>
<td align="left">No</td>
<td align="left">没有</td>
</tr>
<tr>
<td align="left">msgNoFilesSelected</td>
<td align="left">No files selected</td>
<td align="left">“”</td>
</tr>
<tr>
<td align="left">msgCancelled</td>
<td align="left">Cancelled</td>
<td align="left">取消</td>
</tr>
<tr>
<td align="left">msgZoomModalHeading</td>
<td align="left">Detailed Preview</td>
<td align="left">详细预览</td>
</tr>
<tr>
<td align="left">msgSizeTooSmall</td>
<td align="left">File "{name}" (<b>{size} KB</b>) is too small and must be larger than <b>{minSize} KB</b>.</td>
<td align="left">File "{name}" (<b>{size} KB</b>) is too small and must be larger than <b>{minSize} KB</b>.</td>
</tr>
<tr>
<td align="left">msgSizeTooLarge</td>
<td align="left">File "{name}" (<b>{size} KB</b>) exceeds maximum allowed upload size of <b>{maxSize} KB</b>.</td>
<td align="left">文件 "{name}" (<b>{size} KB</b>) 超过了允许大小 <b>{maxSize} KB</b>.</td>
</tr>
<tr>
<td align="left">msgFilesTooLess</td>
<td align="left">You must select at least <b>{n}</b> {files} to upload.</td>
<td align="left">你必须选择最少 <b>{n}</b> {files} 来上传.</td>
</tr>
<tr>
<td align="left">msgFilesTooMany</td>
<td align="left">Number of files selected for upload <b>({n})</b> exceeds maximum allowed limit of <b>{m}</b>.</td>
<td align="left">选择的上传文件个数 <b>({n})</b> 超出最大文件的限制个数 <b>{m}</b>.</td>
</tr>
<tr>
<td align="left">msgFileNotFound</td>
<td align="left">File "{name}" not found!</td>
<td align="left">文件 "{name}" 未找到!</td>
</tr>
<tr>
<td align="left">msgFileSecured</td>
<td align="left">Security restrictions prevent reading the file "{name}".</td>
<td align="left">安全限制，为了防止读取文件 "{name}".</td>
</tr>
<tr>
<td align="left">msgFileNotReadable</td>
<td align="left">File "{name}" is not readable.</td>
<td align="left">文件 "{name}" 不可读.</td>
</tr>
<tr>
<td align="left">msgFilePreviewAborted</td>
<td align="left">File preview aborted for "{name}".</td>
<td align="left">取消 "{name}" 的预览.</td>
</tr>
<tr>
<td align="left">msgFilePreviewError</td>
<td align="left">An error occurred while reading the file "{name}".</td>
<td align="left">读取 "{name}" 时出现了一个错误.</td>
</tr>
<tr>
<td align="left">msgInvalidFileName</td>
<td align="left">Invalid or unsupported characters in file name "{name}".</td>
<td align="left">Invalid or unsupported characters in file name "{name}".</td>
</tr>
<tr>
<td align="left">msgInvalidFileType</td>
<td align="left">Invalid type for file "{name}". Only "{types}" files are supported.</td>
<td align="left">不正确的类型 "{name}". 只支持 "{types}" 类型的文件.</td>
</tr>
<tr>
<td align="left">msgInvalidFileExtension</td>
<td align="left">Invalid extension for file "{name}". Only "{extensions}" files are supported.</td>
<td align="left">不正确的文件扩展名 "{name}". 只支持 "{extensions}" 的文件扩展名.</td>
</tr>
<tr>
<td align="left">msgFileTypes</td>
<td align="left">{'image': 'image','html': 'HTML','text': 'text','video': 'video','audio': 'audio','flash': 'flash','pdf': 'PDF','object': 'object'},</td>
<td align="left">{'image': 'image','html': 'HTML','text': 'text','video': 'video','audio': 'audio','flash': 'flash','pdf': 'PDF','object': 'object'},</td>
</tr>
<tr>
<td align="left">msgUploadAborted</td>
<td align="left">The file upload was aborted</td>
<td align="left">该文件上传被中止</td>
</tr>
<tr>
<td align="left">msgUploadThreshold</td>
<td align="left">Processing...</td>
<td align="left">Processing...</td>
</tr>
<tr>
<td align="left">msgUploadBegin</td>
<td align="left">Initializing...</td>
<td align="left">Initializing...</td>
</tr>
<tr>
<td align="left">msgUploadEnd</td>
<td align="left">Done</td>
<td align="left">Done</td>
</tr>
<tr>
<td align="left">msgUploadEmpty</td>
<td align="left">No valid data available for upload.</td>
<td align="left">No valid data available for upload.</td>
</tr>
<tr>
<td align="left">msgValidationError</td>
<td align="left">Validation Error</td>
<td align="left">验证错误</td>
</tr>
<tr>
<td align="left">msgLoading</td>
<td align="left">Loading file {index} of {files} …</td>
<td align="left">加载第 {index} 文件 共 {files} …</td>
</tr>
<tr>
<td align="left">msgProgress</td>
<td align="left">Loading file {index} of {files} - {name} - {percent}% completed.</td>
<td align="left">加载第 {index} 文件 共 {files} - {name} - {percent}% 完成.</td>
</tr>
<tr>
<td align="left">msgSelected</td>
<td align="left">{n} {files} selected</td>
<td align="left">{n} {files} 选中</td>
</tr>
<tr>
<td align="left">msgFoldersNotAllowed</td>
<td align="left">Drag &amp; drop files only! {n} folder(s) dropped were skipped.</td>
<td align="left">只支持拖拽文件! 跳过 {n} 拖拽的文件夹.</td>
</tr>
<tr>
<td align="left">msgImageWidthSmall</td>
<td align="left">Width of image file "{name}" must be at least {size} px.</td>
<td align="left">宽度的图像文件的"{name}"的必须是至少{size}像素.</td>
</tr>
<tr>
<td align="left">msgImageHeightSmall</td>
<td align="left">Height of image file "{name}" must be at least {size} px.</td>
<td align="left">图像文件的"{name}"的高度必须至少为{size}像素.</td>
</tr>
<tr>
<td align="left">msgImageWidthLarge</td>
<td align="left">Width of image file "{name}" cannot exceed {size} px.</td>
<td align="left">宽度的图像文件"{name}"不能超过{size}像素.</td>
</tr>
<tr>
<td align="left">msgImageHeightLarge</td>
<td align="left">Height of image file "{name}" cannot exceed {size} px.</td>
<td align="left">图像文件"{name}"的高度不能超过{size}像素.</td>
</tr>
<tr>
<td align="left">msgImageResizeError</td>
<td align="left">Could not get the image dimensions to resize.</td>
<td align="left">无法获取的图像尺寸调整。</td>
</tr>
<tr>
<td align="left">msgImageResizeException</td>
<td align="left">Error while resizing the image.&lt;pre&gt;{errors}&lt;/pre&gt;</td>
<td align="left">错误而调整图像大小。&lt;pre&gt;{errors}&lt;/pre&gt;</td>
</tr>
<tr>
<td align="left">msgAjaxError</td>
<td align="left">Something went wrong with the {operation} operation. Please try again later!</td>
<td align="left">Something went wrong with the {operation} operation. Please try again later!</td>
</tr>
<tr>
<td align="left">msgAjaxProgressError</td>
<td align="left">{operation} failed</td>
<td align="left">{operation} failed</td>
</tr>
<tr>
<td align="left">ajaxOperations</td>
<td align="left">{deleteThumb: 'file delete', uploadThumb: 'file upload', uploadBatch: 'batch file upload', uploadExtra: 'form data upload' },</td>
<td align="left">{deleteThumb: 'file delete',uploadThumb: 'file upload', uploadBatch: 'batch file upload',uploadExtra: 'form data upload'},</td>
</tr>
<tr>
<td align="left">dropZoneTitle</td>
<td align="left">Drag &amp; drop files here …</td>
<td align="left">拖拽文件到这里 …<br>支持多文件同时上传</td>
</tr>
<tr>
<td align="left">dropZoneClickTitle</td>
<td align="left">
<br>(or click to select {files})</td>
<td align="left">
<br>(或点击{files}按钮选择文件)</td>
</tr>
<tr>
<td align="left">previewZoomButtonTitles</td>
<td align="left">{prev: 'View previous file',next: 'View next file', toggleheader: 'Toggle header',fullscreen: 'Toggle full screen', borderless: 'Toggle borderless mode', close: 'Close detailed preview' }</td>
<td align="left">{ prev: '预览上一个文件',next: '预览下一个文件',toggleheader: '缩放', fullscreen: '全屏', borderless: '无边界模式',close: '关闭当前预览'}</td>
</tr>
<tr>
<td align="left">fileActionSettings</td>
<td align="left"> </td>
<td align="left">{ removeTitle: '删除文件',uploadTitle: '上传文件',zoomTitle: '查看详情',dragTitle: '移动 / 重置',indicatorNewTitle: '没有上传', indicatorSuccessTitle: '上传',indicatorErrorTitle: '上传错误', indicatorLoadingTitle: '上传 ...'},</td>
</tr>
</tbody>
</table>
<h3 id="item-1-5">五、Method说明</h3>
<table>
<thead><tr>
<th align="left">方法名</th>
<th align="left">描述</th>
</tr></thead>
<tbody>
<tr>
<td align="left">fileerror</td>
<td align="left">异步上传错误结果处理$('#uploadfile').on('fileerror', function(event, data, msg) {});</td>
</tr>
<tr>
<td align="left">fileuploaded</td>
<td align="left">异步上传成功结果处理$("#uploadfile").on("fileuploaded", function (event, data, previewId, index) {})</td>
</tr>
<tr>
<td align="left">filebatchuploaderror</td>
<td align="left">批量上传错误结果处理$('#uploadfile').on('filebatchuploaderror', function(event, data, msg) {});</td>
</tr>
<tr>
<td align="left">filebatchuploadsuccess</td>
<td align="left">批量上传成功结果处理$('#uploadfile').on('filepreupload', function(event, data, previewId, index) {});</td>
</tr>
<tr>
<td align="left">filebatchselected</td>
<td align="left">选择文件后处理事件$("#fileinput").on("filebatchselected", function(event, files) {});</td>
</tr>
<tr>
<td align="left">upload</td>
<td align="left">文件上传方法$("#fileinput").fileinput("upload");</td>
</tr>
<tr>
<td align="left">fileuploaded</td>
<td align="left">上传成功后处理方法$("#fileinput").on("fileuploaded", function(event, data, previewId, index) {});</td>
</tr>
<tr>
<td align="left">filereset</td>
<td align="left"> </td>
</tr>
<tr>
<td align="left">fileclear</td>
<td align="left">点击浏览框右上角X 清空文件前响应事件$("#fileinput").on("fileclear",function(event, data, msg){});</td>
</tr>
<tr>
<td align="left">filecleared</td>
<td align="left">点击浏览框右上角X 清空文件后响应事件$("#fileinput").on("filecleared",function(event, data, msg){});</td>
</tr>
<tr>
<td align="left">fileimageuploaded</td>
<td align="left">在预览框中图片已经完全加载完毕后回调的事件</td>
</tr>
</tbody>
</table>