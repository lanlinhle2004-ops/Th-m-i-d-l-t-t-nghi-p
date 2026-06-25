<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Thư Mời Lễ Tốt Nghiệp</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f0faf9;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* KHÔNG GIAN PHONG BÌ */
        .envelope-container {
            position: relative;
            width: 380px;
            height: 260px;
            cursor: pointer;
            transition: transform 0.3s ease;
            z-index: 10;
        }
        .envelope-container:hover {
            transform: scale(1.03);
        }
        .envelope {
            position: relative;
            width: 100%;
            height: 100%;
            background-color: #81D8D0; /* Màu Tiffany Blue */
            border-radius: 0 0 12px 12px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
        }
        /* Nắp phong bì */
        .flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 0;
            border-left: 190px solid transparent;
            border-right: 190px solid transparent;
            border-top: 140px solid #6fc4bc; /* Màu tiffany đậm hơn chút tạo khối */
            border-radius: 12px 12px 0 0;
            transform-origin: top;
            transition: transform 0.4s ease-in-out, z-index 0.2s ease-in-out;
            z-index: 4;
        }
        /* Mặt trước phong bì túi */
        .pocket {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 0;
            border-left: 190px solid #9be3dc;
            border-right: 190px solid #9be3dc;
            border-bottom: 140px solid #81D8D0;
            border-radius: 0 0 12px 12px;
            z-index: 3;
        }
        /* Chiếc tem tròn dán phong bì */
        .sticker {
            position: absolute;
            top: 120px;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 50px;
            height: 50px;
            background: #fff;
            color: #1a365d;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            z-index: 5;
            transition: opacity 0.3s ease;
        }
        .hint-text {
            position: absolute;
            bottom: -40px;
            width: 100%;
            text-align: center;
            color: #5a9e96;
            font-weight: bold;
            font-size: 14px;
            letter-spacing: 1px;
        }

        /* TRẠNG THÁI MỞ PHONG BÌ */
        .envelope-container.open .flap {
            transform: rotateX(180deg);
            z-index: 1;
        }
        .envelope-container.open .sticker {
            opacity: 0;
            pointer-events: none;
        }

        /* LÁ THƯ BÊN TRONG */
        .letter {
            position: absolute;
            bottom: 10px;
            left: 5%;
            width: 90%;
            height: 90%;
            background-color: #FFF2A3; /* Màu vàng trứng gà nhẹ nhàng, sang trọng */
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0,0,0,0.05);
            z-index: 2;
            transition: all 0.6s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            opacity: 0.8;
        }

        /* Khi phong bì mở, lá thư trượt lên và phóng to chiếm màn hình */
        .envelope-container.open .letter {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(1);
            width: 450px;
            height: auto;
            max-height: 90vh;
            max-width: 95vw;
            z-index: 100;
            opacity: 1;
            box-shadow: 0 20px 50px rgba(0,0,0,0.15);
            overflow-y: auto;
            border: 3px double #e0a910;
        }

        /* NỘI DUNG LÁ THƯ */
        .letter-content {
            color: #4a3b00;
            text-align: center;
        }
        .letter-title {
            font-size: 22px;
            text-transform: uppercase;
            color: #b58100;
            margin-bottom: 15px;
            letter-spacing: 1px;
            font-weight: bold;
        }
        .salutation {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 12px;
            color: #1a365d;
        }
        .dynamic-msg {
            font-size: 15px;
            line-height: 1.6;
            margin-bottom: 20px;
            text-align: justify;
        }
        .event-info {
            background: rgba(255, 255, 255, 0.5);
            padding: 12px;
            border-radius: 6px;
            font-size: 14px;
            text-align: left;
            margin-bottom: 20px;
            border-left: 4px solid #b58100;
        }
        .event-info p {
            margin-bottom: 5px;
        }

        /* PHẦN TƯƠNG TÁC: RSVP & LỜI NHẮN */
        .rsvp-section {
            margin-top: 15px;
            border-top: 1px dashed #e0a910;
            padding-top: 15px;
        }
        .rsvp-title {
            font-size: 14px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .rsvp-options {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 15px;
        }
        .rsvp-btn {
            padding: 8px 18px;
            border: 2px solid #b58100;
            background: transparent;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            color: #b58100;
            transition: all 0.2s;
        }
        .rsvp-btn.active {
            background: #b58100;
            color: #fff;
        }
        .comment-box {
            width: 100%;
            height: 70px;
            padding: 8px;
            border: 1px solid #d1b46a;
            border-radius: 6px;
            background: rgba(255, 255, 255, 0.7);
            font-family: inherit;
            font-size: 13px;
            resize: none;
            margin-bottom: 15px;
            outline: none;
        }
        .comment-box:focus {
            border-color: #b58100;
            background: #fff;
        }
        .submit-btn {
            background: #1a365d;
            color: #fff;
            border: none;
            padding: 10px 25px;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .submit-btn:hover {
            background: #2a4975;
        }

        /* Overlay mờ phía sau khi thư phóng to */
        .overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.3);
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s ease;
            z-index: 90;
        }
        .envelope-container.open ~ .overlay {
            opacity: 1;
        }
    </style>
</head>
<body>

    <div class="envelope-container" id="envelopeContainer" onclick="openEnvelope()">
        <div class="envelope">
            <div class="flap"></div>
            <div class="sticker">🎓</div>
            <div class="pocket"></div>
            
            <div class="letter" onclick="event.stopPropagation();">
                <div class="letter-content">
                    <div class="letter-title">Trân Trọng Kính Mời</div>
                    
                    <div class="salutation" id="guestName">Chào Bạn Mến Thương,</div>
                    <p class="dynamic-msg" id="guestMessage">
                        Lời nhắn mặc định: Trân trọng mời bạn đến tham dự lễ tốt nghiệp của mình. Sự hiện diện của bạn là niềm vinh hạnh lớn của mình!
                    </p>

                    <div class="event-info">
                        <p><strong>⏱ Thời gian:</strong> 08:00 Sáng, Ngày 15/07/2026</p>
                        <p><strong>📍 Địa điểm:</strong> Hội trường lớn - Đại học Quốc Gia</p>
                    </div>

                    <div class="rsvp-section">
                        <p class="rsvp-title">Bạn sẽ tham dự cùng mình chứ? ✨</p>
                        <div class="rsvp-options">
                            <button class="rsvp-btn" id="btnYes" onclick="selectRsvp('Yes')">Sẽ Tham Dự</button>
                            <button class="rsvp-btn" id="btnNo" onclick="selectRsvp('No')">Rất Tiếc Không Thể</button>
                        </div>
                        
                        <textarea class="comment-box" id="guestComment" placeholder="Gửi lời chúc hoặc nhắn nhủ cho mình tại đây nhé..."></textarea>
                        
                        <button class="submit-btn" onclick="sendResponse()">Xác Nhận</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="hint-text" id="hintText">BẤM VÀO ĐỂ MỞ THƯ ❤️</div>
    </div>

    <div class="overlay" onclick="closeEnvelope()"></div>

    <script>
        // 1. Hiệu ứng Mở / Đóng phong bì
        function openEnvelope() {
            document.getElementById('envelopeContainer').classList.add('open');
            document.getElementById('hintText').style.opacity = '0';
        }
        function closeEnvelope() {
            document.getElementById('envelopeContainer').classList.remove('open');
            document.getElementById('hintText').style.opacity = '1';
        }

        // 2. Tự động lấy nội dung từ đường Link (URL Parameters)
        window.onload = function() {
            const urlParams = new URLSearchParams(window.location.search);
            
            // Lấy tham số 'to' (Tên người nhận)
            const to = urlParams.get('to');
            if (to) {
                document.getElementById('guestName').innerText = "Thân gửi " + to + ",";
            }
            
            // Lấy tham số 'msg' (Lời nhắn riêng cho người đó)
            const msg = urlParams.get('msg');
            if (msg) {
                document.getElementById('guestMessage').innerText = msg;
            }
        }

        // 3. Xử lý nút chọn Tham dự / Không tham dự
        let selectedStatus = "";
        function selectRsvp(status) {
            selectedStatus = status;
            if (status === 'Yes') {
                document.getElementById('btnYes').classList.add('active');
                document.getElementById('btnNo').classList.remove('active');
            } else {
                document.getElementById('btnNo').classList.add('active');
                document.getElementById('btnYes').classList.remove('active');
            }
        }

        // 4. Xử lý khi khách bấm nút "Xác Nhận" phản hồi
        function sendResponse() {
            if (!selectedStatus) {
                alert("Vui lòng chọn trạng thái tham dự giúp mình nhé!");
                return;
            }
            const comment = document.getElementById('guestComment').value;
            
            // Hiện tại hiển thị thông báo cảm ơn (Bạn có thể kết nối phần này với Google Form nếu muốn lưu dữ liệu tự động)
            alert("Cảm ơn bạn đã phản hồi! Lựa chọn của bạn: " + (selectedStatus === 'Yes' ? 'Sẽ Tham Dự' : 'Không Thể Tham Dự') + "\nLời nhắn: " + comment);
        }
    </script>
</body>
</html>
