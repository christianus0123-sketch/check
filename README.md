<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>오늘의 아침 확인</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;700&display=swap" rel="stylesheet">
    <style>body { font-family: 'Noto Sans KR', sans-serif; }</style>
</head>
<body class="bg-slate-50 flex items-center justify-center min-h-screen p-4">
    <div class="bg-white p-8 rounded-2xl shadow-xl w-full max-w-md">
        <h1 class="text-2xl font-bold text-center text-indigo-600 mb-6">☀️ 좋은 아침입니다!</h1>
        <form id="attendanceForm" class="space-y-4">
            <div>
                <label class="block text-sm font-medium text-gray-700">학번 (예시: 2101)</label>
                <input type="number" id="studentId" placeholder="2101" class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-indigo-400 outline-none" required>
            </div>
            <div>
                <label class="block text-sm font-medium text-gray-700">이름</label>
                <input type="text" id="name" class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-indigo-400 outline-none" required>
            </div>
            <div>
                <label class="block text-sm font-medium text-gray-700">오늘의 기분</label>
                <div class="flex justify-between mt-2">
                    <label class="cursor-pointer text-2xl hover:scale-125 transition"><input type="radio" name="mood" value="🥰" class="hidden" required> 🥰</label>
                    <label class="cursor-pointer text-2xl hover:scale-125 transition"><input type="radio" name="mood" value="🙂" class="hidden"> 🙂</label>
                    <label class="cursor-pointer text-2xl hover:scale-125 transition"><input type="radio" name="mood" value="😐" class="hidden"> 😐</label>
                    <label class="cursor-pointer text-2xl hover:scale-125 transition"><input type="radio" name="mood" value="😥" class="hidden"> 😥</label>
                    <label class="cursor-pointer text-2xl hover:scale-125 transition"><input type="radio" name="mood" value="😡" class="hidden"> 😡</label>
                </div>
            </div>
            <div>
                <label class="block text-sm font-medium text-gray-700">오늘의 목표</label>
                <input type="text" id="goal" class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-indigo-400 outline-none" placeholder="한 줄 다짐">
            </div>
            <div class="flex items-center space-x-2">
                <input type="checkbox" id="consult" class="w-5 h-5 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500">
                <label for="consult" class="text-sm font-semibold text-rose-500">선생님과 상담하고 싶어요</label>
            </div>
            <button type="submit" class="w-full bg-indigo-600 text-white font-bold py-3 rounded-lg hover:bg-indigo-700 transition shadow-md">출석 체크 완료</button>
        </form>
    </div>
    <script>
        const url = 'URL_HERE';
        document.getElementById('attendanceForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const data = {
                studentId: document.getElementById('studentId').value,
                name: document.getElementById('name').value,
                mood: document.querySelector('input[name="mood"]:checked').value,
                goal: document.getElementById('goal').value,
                consult: document.getElementById('consult').checked ? "신청" : "미신청"
            };
            try {
                await fetch(url, { method: 'POST', body: JSON.stringify(data) });
                alert('정상적으로 기록되었습니다.');
                location.reload();
            } catch (err) { alert('오류가 발생했습니다.'); }
        });
    </script>
</body>
</html>
