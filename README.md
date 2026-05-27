<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>六一儿童节呆呆版</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }
        body {
            background-color: #fff0f5;
            padding: 20px;
        }
        h1 {
            text-align: center;
            color: #ff69b4;
            margin-bottom: 20px;
            font-size: 28px;
        }
        #giftBox {
            width: 320px;
            height: 260px;
            margin: 0 auto 20px auto;
            background: #ffb6c1;
            border-radius: 12px;
            position: relative;
            cursor: pointer;
            box-shadow: 0 6px 15px rgba(255, 105, 180, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            font-weight: bold;
        }
        #giftBox::before {
            content: "";
            position: absolute;
            width: 20px;
            height: 100%;
            background: #fff;
            left: 50%;
            transform: translateX(-50%);
        }
        #giftBox.open {
            height: 0;
            opacity: 0;
            pointer-events: none;
            transition: all 0.5s ease;
        }
        #openBtn {
            display: block;
            margin: 0 auto 20px auto;
            padding: 12px 30px;
            background: #ff69b4;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
        }
        #mainWrap {
            max-width: 800px;
            margin: 0 auto;
            display: none;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }
        .panel {
            width: 360px;
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .item {
            margin-bottom: 16px;
        }
        label {
            display: block;
            color: #333;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .file-wrap {
            position: relative;
            overflow: hidden;
            display: inline-block;
            width: 100%;
        }
        .file-btn {
            display: inline-block;
            width: 100%;
            padding: 12px 20px;
            background: #ff69b4;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            text-align: center;
        }
        .file-wrap input[type=file] {
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            cursor: pointer;
        }
        .file-tip {
            margin-top: 8px;
            font-size: 13px;
            color: #666;
        }
        textarea, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #eee;
            border-radius: 8px;
            font-size: 14px;
        }
        textarea {
            height: 100px;
            resize: none;
        }
        .btn {
            width: 100%;
            padding: 12px;
            margin-top: 8px;
            background: #ff69b4;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
        }
        .btn-gray {
            background: #999;
        }
        .card {
            width: 100%;
            min-height: 420px;
            padding: 15px;
            border-radius: 12px;
            background: linear-gradient(135deg, #ffe4e1, #fff0f5);
            text-align: center;
        }
        .media {
            width: 100%;
            height: 220px;
            border-radius: 8px;
            margin-bottom: 15px;
            background: #f5f5f5;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        .media img, .media video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .card-text {
            font-size: 16px;
            line-height: 1.8;
            color: #333;
        }
        .link-box {
            margin-top: 15px;
            padding: 10px;
            background: #f5f5f5;
            border-radius: 8px;
            display: none;
        }
        .short-link {
            color: #2196f3;
            cursor: pointer;
            word-break: break-all;
        }
    </style>
</head>
<body>
    <h1>🎁 六一儿童节呆呆版</h1>
    <div id="giftBox">点击开启礼物</div>
    <button id="openBtn">点击开启礼物（备用）</button>
    <div id="mainWrap">
        <div class="panel">
            <div class="item">
                <label>📷 上传照片/视频（支持多选）</label>
                <div class="file-wrap">
                    <span class="file-btn">点击选择文件</span>
                    <input type="file" id="fileInput" accept="image/*,video/*" multiple>
                </div>
                <div class="file-tip" id="fileTip">未选择任何文件</div>
            </div>
            <div class="item">
                <label>✍️ 编辑祝福语</label>
                <textarea id="wishText">六一儿童节快乐！愿你永远保持童心，被世界温柔以待。</textarea>
            </div>
            <div class="item">
                <label>🎨 文字颜色</label>
                <select id="colorSel">
                    <option value="#333">黑色</option>
                    <option value="#ff69b4" selected>粉色</option>
                    <option value="#2196f3">蓝色</option>
                    <option value="#4caf50">绿色</option>
                </select>
            </div>
            <button class="btn" id="updateBtn">更新预览</button>
            <button class="btn" id="linkBtn">生成分享链接</button>
            <button class="btn btn-gray" id="resetBtn">重置内容</button>
            <div class="link-box" id="linkBox">
                <p>专属分享链接：</p>
                <p class="short-link" id="shortLink"></p>
            </div>
        </div>
        <div class="panel">
            <div class="card">
                <div class="media" id="mediaBox">请上传素材</div>
                <div class="card-text" id="cardText">六一儿童节快乐！愿你永远保持童心，被世界温柔以待。</div>
            </div>
        </div>
    </div>
<script>
    const giftBox = document.getElementById('giftBox');
    const openBtn = document.getElementById('openBtn');
    const mainWrap = document.getElementById('mainWrap');
    const fileInput = document.getElementById('fileInput');
    const fileTip = document.getElementById('fileTip');
    const wishText = document.getElementById('wishText');
    const colorSel = document.getElementById('colorSel');
    const updateBtn = document.getElementById('updateBtn');
    const linkBtn = document.getElementById('linkBtn');
    const resetBtn = document.getElementById('resetBtn');
    const mediaBox = document.getElementById('mediaBox');
    const cardText = document.getElementById('cardText');
    const linkBox = document.getElementById('linkBox');
    const shortLink = document.getElementById('shortLink');
    let mediaList = [];

    function compressImage(file) {
        return new Promise(resolve => {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = e => {
                const img = new Image();
                img.src = e.target.result;
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    const ctx = canvas.getContext('2d');
                    canvas.width = 400;
                    canvas.height = img.height * (400 / img.width);
                    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
                    resolve(canvas.toDataURL('image/jpeg', 0.6));
                }
            }
        })
    }

    function openGift() {
        giftBox.classList.add('open');
        mainWrap.style.display = 'flex';
        cardText.innerText = wishText.value;
        cardText.style.color = colorSel.value;
    }

    giftBox.addEventListener('click', openGift);
    giftBox.addEventListener('touchstart', openGift);
    openBtn.addEventListener('click', openGift);

    fileInput.addEventListener('change', async e => {
        const files = e.target.files;
        if (!files.length) return;
        fileTip.innerText = `已选择 ${files.length} 个文件`;
        mediaList = [];
        for (let file of files) {
            if (file.type.startsWith('image/')) {
                const dataUrl = await compressImage(file);
                mediaList.push({ type: 'image', src: dataUrl });
            } else if (file.type.startsWith('video/')) {
                mediaList.push({ type: 'video', src: URL.createObjectURL(file) });
            }
        }
    });

    updateBtn.addEventListener('click', () => {
        cardText.innerText = wishText.value;
        cardText.style.color = colorSel.value;
        if (mediaList.length > 0) {
            const first = mediaList[0];
            if (first.type === 'image') {
                mediaBox.innerHTML = `<img src="${first.src}">`;
            } else {
                mediaBox.innerHTML = `<video src="${first.src}" controls></video>`;
            }
        }
    });

    resetBtn.addEventListener('click', () => {
        fileInput.value = '';
        wishText.value = '六一儿童节快乐！愿你永远保持童心，被世界温柔以待。';
        colorSel.value = '#ff69b4';
        mediaBox.innerHTML = '请上传素材';
        cardText.innerText = wishText.value;
        cardText.style.color = colorSel.value;
        fileTip.innerText = '未选择任何文件';
        mediaList = [];
        linkBox.style.display = 'none';
   
