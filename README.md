<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>แบบประเมินความเสี่ยงโรคหลอดเลือดสมอง</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            line-height: 1.6;
        }
        .question {
            margin-bottom: 15px;
        }
        .question label {
            display: block;
        }
        button {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>แบบประเมินความเสี่ยงโรคหลอดเลือดสมอง</h1>
    <form id="strokeRiskForm">
        <div class="question">
            <label>อายุของคุณ:</label>
            <label><input type="radio" name="age" value="0"> น้อยกว่า 45 ปี</label>
            <label><input type="radio" name="age" value="1"> 45-54 ปี</label>
            <label><input type="radio" name="age" value="2"> 55-64 ปี</label>
            <label><input type="radio" name="age" value="3"> 65 ปีขึ้นไป</label>
        </div>
        <div class="question">
            <label>เพศ:</label>
            <label><input type="radio" name="gender" value="1"> ชาย</label>
            <label><input type="radio" name="gender" value="0"> หญิง</label>
        </div>
        <div class="question">
            <label>มีประวัติคนในครอบครัวเป็นโรคหลอดเลือดสมองหรือไม่?</label>
            <label><input type="radio" name="familyHistory" value="2"> ใช่</label>
            <label><input type="radio" name="familyHistory" value="0"> ไม่ใช่</label>
        </div>
        <div class="question">
            <label>คุณมีโรคประจำตัวใดบ้าง? (เลือกได้หลายข้อ)</label>
            <label><input type="checkbox" name="conditions" value="2"> โรคความดันโลหิตสูง</label>
            <label><input type="checkbox" name="conditions" value="2"> โรคเบาหวาน</label>
            <label><input type="checkbox" name="conditions" value="3"> โรคหัวใจ</label>
            <label><input type="checkbox" name="conditions" value="2"> คอเลสเตอรอลสูง</label>
            <label><input type="checkbox" name="conditions" value="1"> โรคอ้วน</label>
            <label><input type="checkbox" name="conditions" value="0"> ไม่มีโรคประจำตัว</label>
        </div>
        <div class="question">
            <label>คุณสูบบุหรี่หรือไม่?</label>
            <label><input type="radio" name="smoking" value="2"> สูบ</label>
            <label><input type="radio" name="smoking" value="0"> ไม่สูบ</label>
        </div>
        <div class="question">
            <label>การดื่มแอลกอฮอล์ของคุณเป็นประจำหรือไม่?</label>
            <label><input type="radio" name="alcohol" value="1"> ดื่ม</label>
            <label><input type="radio" name="alcohol" value="0"> ไม่ดื่ม</label>
        </div>
        <button type="button" onclick="calculateRisk()">ประเมินผล</button>
        <div class="result" id="result"></div>
    </form>

    <script>
        function calculateRisk() {
            let form = document.forms['strokeRiskForm'];
            let totalScore = 0;

            totalScore += parseInt(form.age.value || 0);
            totalScore += parseInt(form.gender.value || 0);
            totalScore += parseInt(form.familyHistory.value || 0);

            let conditions = form['conditions'];
            for (let condition of conditions) {
                if (condition.checked) {
                    totalScore += parseInt(condition.value);
                }
            }

            totalScore += parseInt(form.smoking.value || 0);
            totalScore += parseInt(form.alcohol.value || 0);

            let result = document.getElementById('result');
            if (totalScore <= 5) {
                result.textContent = `คะแนนรวม: ${totalScore} (ความเสี่ยงต่ำ)`;
            } else if (totalScore <= 12) {
                result.textContent = `คะแนนรวม: ${totalScore} (ความเสี่ยงปานกลาง)`;
            } else {
                result.textContent = `คะแนนรวม: ${totalScore} (ความเสี่ยงสูง)`;
            }
        }
    </script>
</body>
</html>
