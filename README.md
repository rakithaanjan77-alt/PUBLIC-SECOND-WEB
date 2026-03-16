# PUBLIC-SECOND-WEB
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>iFIXpath | Strategic Numerology Lab</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background: #020617; color: white; font-family: 'Inter', sans-serif; }
        .glass { background: rgba(15, 23, 42, 0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.1); }
        .logo-container img { max-width: 280px; margin: 0 auto; filter: drop-shadow(0 0 10px rgba(34, 211, 238, 0.2)); }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4">

    <div class="glass p-8 rounded-[2rem] shadow-2xl w-full max-w-lg text-center border border-slate-800">
        
        <div class="logo-container mb-6">
            <div class="bg-white/5 p-4 rounded-2xl inline-block">
                <h1 class="text-3xl font-bold text-white uppercase tracking-tighter">iFIX<span class="text-orange-500">path</span></h1>
                <p class="text-[10px] text-cyan-500 tracking-[0.3em] font-bold mt-1">STRATEGIC SOLUTIONS</p>
            </div>
        </div>

        <div class="space-y-5 text-left">
            <div>
                <label class="text-[10px] text-slate-500 ml-1 mb-1 block font-bold uppercase tracking-widest text-center">Business Name</label>
                <input type="text" id="bizName" placeholder="e.g. iFIXpath" 
                    class="w-full p-4 rounded-2xl bg-slate-900/80 border border-slate-700 focus:outline-none focus:border-orange-500 transition-all text-lg text-center font-semibold">
            </div>

            <div>
                <label class="text-[10px] text-slate-500 ml-1 mb-1 block font-bold uppercase tracking-widest text-center">Owner's Birthday</label>
                <input type="date" id="birthDate" 
                    class="w-full p-4 rounded-2xl bg-slate-900/80 border border-slate-700 focus:outline-none focus:border-cyan-500 transition-all text-lg text-slate-300 text-center">
            </div>
            
            <button onclick="checkCompatibility()" 
                class="w-full bg-gradient-to-r from-orange-600 to-orange-500 hover:from-orange-500 hover:to-orange-400 text-white font-black py-5 rounded-2xl transition-all shadow-[0_0_20px_rgba(234,88,12,0.3)] transform hover:scale-[1.02] uppercase tracking-widest text-sm">
                Analyze Alignment
            </button>
        </div>

        <div id="resultArea" class="mt-10 hidden border-t border-slate-800/50 pt-8 animate-fade-in">
            <div class="grid grid-cols-2 gap-4 mb-6 text-center">
                <div class="p-4 bg-slate-900/40 rounded-3xl border border-slate-800">
                    <div class="text-[9px] text-slate-500 uppercase font-bold tracking-widest">Business</div>
                    <div id="bizNumDisplay" class="text-5xl font-black text-orange-500"></div>
                </div>
                <div class="p-4 bg-slate-900/40 rounded-3xl border border-slate-800">
                    <div class="text-[9px] text-slate-500 uppercase font-bold tracking-widest">Owner</div>
                    <div id="ownerNumDisplay" class="text-5xl font-black text-cyan-400"></div>
                </div>
            </div>

            <div class="mb-6 px-4">
                <div class="flex justify-between text-[10px] text-slate-500 mb-2 font-bold uppercase tracking-widest">
                    <span>Alignment Score</span>
                    <span id="scoreText">0%</span>
                </div>
                <div class="w-full bg-slate-800 rounded-full h-2">
                    <div id="scoreBar" class="bg-gradient-to-r from-orange-500 to-cyan-400 h-2 rounded-full transition-all duration-1000" style="width: 0%"></div>
                </div>
            </div>

            <div id="advice" class="text-sm text-slate-300 font-medium leading-relaxed bg-white/5 p-4 rounded-2xl italic border border-white/5"></div>
        </div>
    </div>

    <script>
        function getNumerologyNumber(val) {
            let n = val;
            while (n > 9 && n !== 11 && n !== 22 && n !== 33) {
                n = n.toString().split('').reduce((acc, d) => acc + parseInt(d), 0);
            }
            return n;
        }

        function checkCompatibility() {
            const bizInput = document.getElementById('bizName').value;
            const bdayInput = document.getElementById('birthDate').value;

            if (!bizInput || !bdayInput) return alert("Fill both fields, machan!");

            const cleanName = bizInput.toUpperCase().replace(/[^A-Z]/g, '');
            const chart = {'A':1,'B':2,'C':3,'D':4,'E':5,'F':6,'G':7,'H':8,'I':9,'J':1,'K':2,'L':3,'M':4,'N':5,'O':6,'P':7,'Q':8,'R':9,'S':1,'T':2,'U':3,'V':4,'W':5,'X':6,'Y':7,'Z':8};
            
            let bizSum = 0;
            for (let char of cleanName) bizSum += chart[char] || 0;
            const bizFinal = getNumerologyNumber(bizSum);

            const dateDigits = bdayInput.replace(/-/g, '');
            let ownerSum = 0;
            for (let digit of dateDigits) ownerSum += parseInt(digit);
            const ownerFinal = getNumerologyNumber(ownerSum);

            let score = 0;
            let advice = "";

            if (bizFinal === ownerFinal) {
                score = 100;
                advice = "Perfect Harmony! You and this business name vibrate on the same frequency. Success is imminent.";
            } else if ([1, 3, 5, 9].includes(bizFinal) && [1, 3, 5, 9].includes(ownerFinal)) {
                score = 85;
                advice = "Great Dynamic Alignment. Both numbers represent growth and energy. A strong path forward.";
            } else {
                score = 70;
                advice = "Balanced Alignment. Your personal strengths will complement this business structure well.";
            }

            document.getElementById('resultArea').style.display = 'block';
            document.getElementById('bizNumDisplay').innerText = bizFinal;
            document.getElementById('ownerNumDisplay').innerText = ownerFinal;
            
            setTimeout(() => {
                document.getElementById('scoreBar').style.width = score + "%";
                document.getElementById('scoreText').innerText = score + "%";
                document.getElementById('advice').innerText = '"' + advice + '"';
            }, 100);
        }
    </script>
</body>
</html>