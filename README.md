<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تنزيل فيديو تيك توك</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        input, button {
            padding: 10px;
            margin: 10px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <h1>تنزيل مقاطع فيديو تيك توك بدون علامة مائية</h1>
    <input type="text" id="tiktokLink" placeholder="أدخل رابط الفيديو هنا" />
    <button onclick="downloadVideo()">تحميل الفيديو</button>
    <br>
    <div id="downloadLink"></div>

    <script>
        function downloadVideo() {
            var videoLink = document.getElementById('tiktokLink').value;
            if (videoLink) {
                fetch('/download?url=' + encodeURIComponent(videoLink))
                .then(response => response.json())
                .then(data => {
                    if (data.success) {
                        var link = document.createElement('a');
                        link.href = data.videoUrl;
                        link.download = 'tiktok_video.mp4';
                        link.innerHTML = 'اضغط هنا لتنزيل الفيديو';
                        document.getElementById('downloadLink').innerHTML = '';
                        document.getElementById('downloadLink').appendChild(link);
                    } else {
                        alert('لم يتم العثور على الفيديو أو حدث خطأ.');
                    }
                })
                .catch(error => alert('خطأ في الاتصال بالخادم.'));
            } else {
                alert('الرجاء إدخال رابط فيديو تيك توك.');
            }
        }
    </script>
</body>
</html>
