# fileinput
一个上传文件的插件



一、引入文件
<link href="../css/bootstrap.min.css"rel="stylesheet">
<link href="../css/fileinput.css" media="all"rel="stylesheet" type="text/css" />
<scriptsrc="../js/jquery-2.0.3.min.js"></script>
<script src="../js/fileinput.js"type="text/javascript"></script>
<script src="../js/bootstrap.min.js"type="text/javascript"></script>



二、初始化设置
//初始化fileinput
initFileInput();
function initFileInput() {
    $("#uploadImg").fileinput({
        language: 'zh', //设置语言
        dropZoneTitle: '可以将图片拖放到这里 …支持多文件上传',
        uploadUrl: "index.php", //上传的地址
        uploadExtraData: function(previewId, index) {   //该插件可以向您的服务器方法发送附加数据。这可以通过uploadExtraData在键值对中设置为关联数组对象来完成。所以如果你有设置uploadExtraData={id:'kv-1'}，在PHP中你可以读取这些数据$_POST['id']
            var id = $('#id').val();
            return {seriesId: id};
        },
        allowedFileExtensions: ['jpg','png'],//接收的文件后缀
        uploadAsync: true, //默认异步上传
        showUpload: true, //是否显示上传按钮
        showRemove: true, //显示移除按钮
        showPreview: true, //是否显示预览
        showCancel:true,   //是否显示文件上传取消按钮。默认为true。只有在AJAX上传过程中，才会启用和显示
        showCaption: true,//是否显示文件标题，默认为true
        browseClass: "btn btn-primary", //文件选择器/浏览按钮的CSS类。默认为btn btn-primary
        dropZoneEnabled: true,//是否显示拖拽区域
        minImageWidth: 50, //图片的最小宽度
        minImageHeight: 50,//图片的最小高度
        maxImageWidth: 1000,//图片的最大宽度
        maxImageHeight: 1000,//图片的最大高度
        maxFileSize: 1024,//单位为kb，如果为0表示不限制文件大小
        minFileCount: 1, //每次上传允许的最少文件数。如果设置为0，则表示文件数是可选的。默认为0
        maxFileCount: 0, //每次上传允许的最大文件数。如果设置为0，则表示允许的文件数是无限制的。默认为0
        previewFileIcon: "<i class='glyphicon glyphicon-king'></i>",//当检测到用于预览的不可读文件类型时，将在每个预览文件缩略图中显示的图标。默认为<i class="glyphicon glyphicon-file"></i>  
        layoutTemplates:{
            actionUpload:''//去除上传预览缩略图中的上传图片
            actionZoom:'',   //去除上传预览缩略图中的查看详情预览的缩略图标
            actionDownload:'' //去除上传预览缩略图中的下载图标
            actionDelete:'', //去除上传预览的缩略图中的删除图标
        },//对象用于渲染布局的每个部分的模板配置。您可以设置以下模板来控制窗口小部件布局.eg:去除上传图标
        msgFilesTooMany: "选择上传的文件数量({n}) 超过允许的最大数值{m}！",//字符串，当文件数超过设置的最大计数时显示的消息 maxFileCount。默认为：选择上传的文件数（{n}）超出了允许的最大限制{m}。请重试您的上传！
    }).on('filebatchpreupload', function(event, data) { //该方法将在上传之前触发
        var id = $('#id option:selected').val();
        if(id == 0){
            return {
                message: "请选择", // 验证错误信息在上传前要显示。如果设置了这个设置，插件会在调用时自动中止上传，并将其显示为错误消息。您可以使用此属性来读取文件并执行自己的自定义验证
                data:{} // any other data to send that can be referred in `filecustomerror`
            };
        }
    });
}
//fileuploaded此事件仅针对ajax上传触发，并在每个缩略图文件上传完成后触发。此事件仅针对ajax上传并在以下情况下触发：当点击每个预览缩略图中的上传图标并且文件上传成功时，或者当你有 uploadAsync设置为true您已触发批量上传。在这种情况下，fileuploaded每一个人选择的文件被上传成功后，触发事件。
var id_str = '';
$('#uploadImg').on('fileuploaded', function(event, data, previewId, index) {
    if(typeof(data.response.id) != 'undefined'){
        id_str = id_str+data.response.id+',';
    }
});
// filebatchuploadcomplete此事件仅在ajax上传和完成同步或异步ajax批量上传后触发。
$('#uploadImg').on('filebatchuploadcomplete',function (event,files,extra) {
    if(id_str.length == 0){
        layer.msg('上传失败', {icon: 0});//弹框提示
        return false;
    }
    setTimeout(function(){ //执行延时关闭
        closeSelf();
    },1000);
});



三、Options 说明
属性名	属性类型	描述说明	默认值
language	String	多语言设置，使用时需提前引入locales文件夹下对应的语言文件，中文zh，引入语言文件必须放在fileinput.js之后	'en'
showCaption	Boolean	是否显示被选文件的简介	true
showBrowse	Boolean	是否显示浏览按钮	true
showPreview	Boolean	是否显示预览区域	true
showRemove	Boolean	是否显示移除按钮	true,
showUpload	Boolean	是否显示上传按钮	true,
showCancel	Boolean	是否显示取消按钮	true,
showClose:	Boolean	是否显示关闭按钮	true
showUploadedThumbs	Boolean		true
browseOnZoneClick	Boolean		false
autoReplace	Boolean	是否自动替换当前图片，设置为true时，再次选择文件， 会将当前的文件替换掉。	false
generateFileId	Object		null
previewClass	String	添加预览按钮的类属性	‘’
captionClass	String		‘’
frameClass	String		'krajee-default'
mainClass	String		'file-caption-main'
mainTemplate	Object		null
purifyHtml	Boolean		true
fileSizeGetter	Object		null
initialCaption	String		''
initialPreview	Array/Object		[]
initialPreviewDelimiter	String		'$$'
initialPreviewAsData	Boolean		false
initialPreviewFileType	String		'image'
initialPreviewConfig	Array/Object		[]
initialPreviewThumbTags	Array/Object		[]
previewThumbTags	Object		{}
initialPreviewShowDelete	Boolean		true
removeFromPreviewOnError	Boolean		false
deleteUrl	String	删除图片时的请求路径	''
deleteExtraData	Object	删除图片时额外传入的参数	{}
overwriteInitial	Boolean		true
previewZoomButtonIcons	Object		{prev: '',next: '',toggleheader: '',fullscreen: '',borderless: '',close: ''},
previewZoomButtonClasses	Object		{prev: 'btn btn-navigate',next: 'btn btn-navigate',toggleheader: 'btn btn-default btn-header-toggle',fullscreen: 'btn btn-default',borderless: 'btn btn-default',close: 'btn btn-default'},
preferIconicPreview	Boolrean		false
preferIconicZoomPreview	Boolrean		false
allowedPreviewTypes	undefined		undefined
allowedPreviewMimeTypes	Object		null
allowedFileTypes	Object	接收的文件后缀，如['jpg', 'gif', 'png'],不填将不限制上传文件后缀类型	null
allowedFileExtensions	Object		null
defaultPreviewContent	Object		null
customLayoutTags	Object		{}
customPreviewTags	Object		{}
previewFileIcon	String		''
previewFileIconClass	String		'file-other-icon'
previewFileIconSettings	Object		{}
previewFileExtSettings	Object		{}
buttonLabelClass	String		'hidden-xs'
browseIcon	String		' '
browseClass	String		'btn btn-primary'
removeIcon	String		''
removeClass	String		'btn btn-default'
cancelIcon	String		''
cancelClass	String		'btn btn-default'
uploadIcon	String		''
uploadClass	String		'btn btn-default'
uploadUrl	String	上传文件路径	null
uploadAsync	boolean	是否为异步上传	true
uploadExtraData		上传文件时额外传递的参数设置	{}
zoomModalHeight	number		480
minImageWidth	String	图片的最小宽度	null
minImageHeight	String	图片的最小高度	null
maxImageWidth	String	图片的最大宽度	null
maxImageHeight	String	图片的最大高度	null
resizeImage	boolean		false
resizePreference	String		'width'
resizeQuality	number		0.92
resizeDefaultImageType	String		'image/jpeg'
minFileSize	number	单位为kb，上传文件的最小大小值	0
maxFileSize	number	单位为kb，如果为0表示不限制文件大小	0
resizeDefaultImageType	number		25600(25MB)
minFileCount	number	表示同时最小上传的文件个数	0
maxFileCount	number	表示允许同时上传的最大文件个数	0
validateInitialCount	boolean		false
msgValidationErrorClass	String		'text-danger'
msgValidationErrorIcon	String		' '
msgErrorClass	String		'file-error-message'
progressThumbClass	String		"progress-bar progress-bar-success progress-bar-striped active"
rogressClass	String		"progress-bar progress-bar-success progress-bar-striped active"
progressCompleteClass	String		"progress-bar progress-bar-success"
progressErrorClass	String		"progress-bar progress-bar-danger"
progressUploadThreshold	number		99
previewFileType	String	预览文件类型,内置['image', 'html', 'text', 'video', 'audio', 'flash', 'object',‘other‘]等格式	'image'
elCaptionContainer	String		null
elCaptionText	String	设置标题栏提示信息	null
elPreviewContainer	String		null
elPreviewImage	String		null
elPreviewStatus	String		null
elErrorContainer	String		null
errorCloseButton	String		'<span class="close kv-error-close">×</span>'
slugCallback	function	选择后未上传前 回调方法	null
dropZoneEnabled	boolean	是否显示拖拽区域	true
dropZoneTitleClass	String	拖拽区域类属性设置	'file-drop-zone-title'
fileActionSettings	Object	设置预览图片的显示样式	{showRemove: true,showUpload: false,showZoom: true,showDrag: true,removeIcon: '',removeClass: 'btn btn-xs btn-default',removeTitle: 'Remove file',uploadIcon: '',uploadClass: 'btn btn-xs btn-default',uploadTitle: 'Upload file',zoomIcon: '',zoomClass: 'btn btn-xs btn-default',zoomTitle: 'View Details',dragIcon: '',dragClass: 'text-info',dragTitle: 'Move / Rearrange',dragSettings: {},indicatorNew: '',indicatorSuccess: '',indicatorError: '',indicatorLoading: '',indicatorNewTitle: 'Not uploaded yet',indicatorSuccessTitle: 'Uploaded',indicatorErrorTitle: 'Upload Error',indicatorLoadingTitle: 'Uploading ...'}
otherActionButtons	String		''
textEncoding	String	编码设置	'UTF-8'
ajaxSettings	Object		{}
ajaxDeleteSettings	Object		{}
showAjaxErrorDetails	boolean		true


四、提示说明设置
属性名	默认值	中文
fileSingle	file	文件
filePlural	files	个文件
browseLabel	Browse &hellip	选择 …
removeLabel	Remove	移除
removeTitle	Clear selected files	清除选中文件
cancelLabel	Cancel	取消
cancelTitle	Abort ongoing upload	取消进行中的上传
uploadLabel	Upload	上传
uploadTitle	Upload selected files	上传选中文件
msgNo	No	没有
msgNoFilesSelected	No files selected	“”
msgCancelled	Cancelled	取消
msgZoomModalHeading	Detailed Preview	详细预览
msgSizeTooSmall	File "{name}" ({size} KB) is too small and must be larger than {minSize} KB.	File "{name}" ({size} KB) is too small and must be larger than {minSize} KB.
msgSizeTooLarge	File "{name}" ({size} KB) exceeds maximum allowed upload size of {maxSize} KB.	文件 "{name}" ({size} KB) 超过了允许大小 {maxSize} KB.
msgFilesTooLess	You must select at least {n} {files} to upload.	你必须选择最少 {n} {files} 来上传.
msgFilesTooMany	Number of files selected for upload ({n}) exceeds maximum allowed limit of {m}.	选择的上传文件个数 ({n}) 超出最大文件的限制个数 {m}.
msgFileNotFound	File "{name}" not found!	文件 "{name}" 未找到!
msgFileSecured	Security restrictions prevent reading the file "{name}".	安全限制，为了防止读取文件 "{name}".
msgFileNotReadable	File "{name}" is not readable.	文件 "{name}" 不可读.
msgFilePreviewAborted	File preview aborted for "{name}".	取消 "{name}" 的预览.
msgFilePreviewError	An error occurred while reading the file "{name}".	读取 "{name}" 时出现了一个错误.
msgInvalidFileName	Invalid or unsupported characters in file name "{name}".	Invalid or unsupported characters in file name "{name}".
msgInvalidFileType	Invalid type for file "{name}". Only "{types}" files are supported.	不正确的类型 "{name}". 只支持 "{types}" 类型的文件.
msgInvalidFileExtension	Invalid extension for file "{name}". Only "{extensions}" files are supported.	不正确的文件扩展名 "{name}". 只支持 "{extensions}" 的文件扩展名.
msgFileTypes	{'image': 'image','html': 'HTML','text': 'text','video': 'video','audio': 'audio','flash': 'flash','pdf': 'PDF','object': 'object'},	{'image': 'image','html': 'HTML','text': 'text','video': 'video','audio': 'audio','flash': 'flash','pdf': 'PDF','object': 'object'},
msgUploadAborted	The file upload was aborted	该文件上传被中止
msgUploadThreshold	Processing...	Processing...
msgUploadBegin	Initializing...	Initializing...
msgUploadEnd	Done	Done
msgUploadEmpty	No valid data available for upload.	No valid data available for upload.
msgValidationError	Validation Error	验证错误
msgLoading	Loading file {index} of {files} …	加载第 {index} 文件 共 {files} …
msgProgress	Loading file {index} of {files} - {name} - {percent}% completed.	加载第 {index} 文件 共 {files} - {name} - {percent}% 完成.
msgSelected	{n} {files} selected	{n} {files} 选中
msgFoldersNotAllowed	Drag & drop files only! {n} folder(s) dropped were skipped.	只支持拖拽文件! 跳过 {n} 拖拽的文件夹.
msgImageWidthSmall	Width of image file "{name}" must be at least {size} px.	宽度的图像文件的"{name}"的必须是至少{size}像素.
msgImageHeightSmall	Height of image file "{name}" must be at least {size} px.	图像文件的"{name}"的高度必须至少为{size}像素.
msgImageWidthLarge	Width of image file "{name}" cannot exceed {size} px.	宽度的图像文件"{name}"不能超过{size}像素.
msgImageHeightLarge	Height of image file "{name}" cannot exceed {size} px.	图像文件"{name}"的高度不能超过{size}像素.
msgImageResizeError	Could not get the image dimensions to resize.	无法获取的图像尺寸调整。
msgImageResizeException	Error while resizing the image.<pre>{errors}</pre>	错误而调整图像大小。<pre>{errors}</pre>
msgAjaxError	Something went wrong with the {operation} operation. Please try again later!	Something went wrong with the {operation} operation. Please try again later!
msgAjaxProgressError	{operation} failed	{operation} failed
ajaxOperations	{deleteThumb: 'file delete', uploadThumb: 'file upload', uploadBatch: 'batch file upload', uploadExtra: 'form data upload' },	{deleteThumb: 'file delete',uploadThumb: 'file upload', uploadBatch: 'batch file upload',uploadExtra: 'form data upload'},
dropZoneTitle	Drag & drop files here …	拖拽文件到这里 …
支持多文件同时上传
dropZoneClickTitle	
(or click to select {files})	
(或点击{files}按钮选择文件)
previewZoomButtonTitles	{prev: 'View previous file',next: 'View next file', toggleheader: 'Toggle header',fullscreen: 'Toggle full screen', borderless: 'Toggle borderless mode', close: 'Close detailed preview' }	{ prev: '预览上一个文件',next: '预览下一个文件',toggleheader: '缩放', fullscreen: '全屏', borderless: '无边界模式',close: '关闭当前预览'}
fileActionSettings		{ removeTitle: '删除文件',uploadTitle: '上传文件',zoomTitle: '查看详情',dragTitle: '移动 / 重置',indicatorNewTitle: '没有上传', indicatorSuccessTitle: '上传',indicatorErrorTitle: '上传错误', indicatorLoadingTitle: '上传 ...'},

五、Method说明
方法名	描述
fileerror	异步上传错误结果处理$('#uploadfile').on('fileerror', function(event, data, msg) {});
fileuploaded	异步上传成功结果处理$("#uploadfile").on("fileuploaded", function (event, data, previewId, index) {})
filebatchuploaderror	批量上传错误结果处理$('#uploadfile').on('filebatchuploaderror', function(event, data, msg) {});
filebatchuploadsuccess	批量上传成功结果处理$('#uploadfile').on('filepreupload', function(event, data, previewId, index) {});
filebatchselected	选择文件后处理事件$("#fileinput").on("filebatchselected", function(event, files) {});
upload	文件上传方法$("#fileinput").fileinput("upload");
fileuploaded	上传成功后处理方法$("#fileinput").on("fileuploaded", function(event, data, previewId, index) {});
filereset	
fileclear	点击浏览框右上角X 清空文件前响应事件$("#fileinput").on("fileclear",function(event, data, msg){});
filecleared	点击浏览框右上角X 清空文件后响应事件$("#fileinput").on("filecleared",function(event, data, msg){});
fileimageuploaded	在预览框中图片已经完全加载完毕后回调的事件