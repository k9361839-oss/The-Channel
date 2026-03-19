<div id="main-app" style="direction: rtl; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; padding: 20px; transition: all 0.3s ease; border: 1px solid #ddd; border-radius: 12px; background-color: #ffffff; color: #000000;">

    <div style="display: flex; justify-content: space-between; align-items: flex-start;">
        <div style="text-align: left; flex: 1;">
            <h1 style="margin: 0; font-size: 2.5rem; color: #008069;">אלעדים על המפה</h1>
            <h3 style="margin: 5px 0; color: #666; font-weight: normal;">204 משתתפים</h3>
        </div>
        
        <div style="display: flex; align-items: center; gap: 15px;">
            <div id="search-circle" title="מעבר להודעה" style="width: 45px; height: 45px; border-radius: 50%; background: #008069; color: white; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 0.8rem; text-align: center; border: 2px solid #fff; box-shadow: 0 2px 5px rgba(0,0,0,0.2);" onclick="goToMessage()">
                מעבר<br>הודעה
            </div>
            <div id="theme-toggle" style="font-size: 2rem; cursor: pointer; user-select: none;" onclick="toggleTheme()">☀️</div>
        </div>
    </div>

    <hr style="border: 0; height: 2px; background: #008069; margin: 20px 0; opacity: 0.5;">

    <div id="messages-container" style="padding: 10px;">
        <div id="msg-1" style="border: 2px solid #008069; border-radius: 15px; padding: 15px; position: relative; max-width: 500px; background: rgba(0, 128, 105, 0.05); transition: background 0.3s;">
            <p style="margin: 0; font-size: 1.1rem; line-height: 1.5;">היי חברים זה האתר של קבוצת הצ'אט אלעדים על המפה מקווים שתהנו</p>
            
            <div style="margin-top: 15px; display: flex; flex-direction: column; gap: 10px;">
                <div id="emoji-trigger" style="cursor: pointer; font-size: 1.3rem; width: fit-content;" onclick="showEmojiPicker()">😊 +</div>
                <div id="emoji-picker" style="display: none; gap: 10px; background: white; padding: 5px; border-radius: 10px; border: 1px solid #ccc; width: fit-content;">
                    <span style="cursor:pointer" onclick="addReaction('👍')">👍</span>
                    <span style="cursor:pointer" onclick="addReaction('❤️')">❤️</span>
                    <span style="cursor:pointer" onclick="addReaction('😂')">😂</span>
                    <span style="cursor:pointer" onclick="addReaction('🔥')">🔥</span>
                </div>
                <div id="reactions-display" style="display: flex; gap: 8px; flex-wrap: wrap;">
                    </div>
            </div>
        </div>
    </div>

</div>

<script>
    let isDarkMode = false;
    const reactions = {};

    function toggleTheme() {
        const app = document.getElementById('main-app');
        const toggle = document.getElementById('theme-toggle');
        isDarkMode = !isDarkMode;

        if (isDarkMode) {
            app.style.backgroundColor = '#121212';
            app.style.color = '#ffffff';
            app.style.borderColor = '#333';
            toggle.innerText = '🌙';
        } else {
            app.style.backgroundColor = '#ffffff';
            app.style.color = '#000000';
            app.style.borderColor = '#ddd';
            toggle.innerText = '☀️';
        }
    }

    function goToMessage() {
        const num = prompt("הקש את מספר ההודעה שאליה תרצה לעבור:");
        if (num) {
            alert("עובר להודעה מספר " + num + "...");
            // בשימוש חי כאן תהיה פונקציית Scroll
        }
    }

    function showEmojiPicker() {
        const picker = document.getElementById('emoji-picker');
        picker.style.display = (picker.style.display === 'none' || picker.style.display === '') ? 'flex' : 'none';
    }

    function addReaction(emoji) {
        if (!reactions[emoji]) {
            reactions[emoji] = 1;
        } else {
            reactions[emoji]++;
        }
        updateReactions();
        document.getElementById('emoji-picker').style.display = 'none';
    }

    function updateReactions() {
        const display = document.getElementById('reactions-display');
        display.innerHTML = '';
        for (const [emoji, count] of Object.entries(reactions)) {
            const span = document.createElement('span');
            span.style = "background: rgba(0,0,0,0.1); padding: 4px 10px; border-radius: 15px; font-size: 0.9rem; font-weight: bold; border: 1px solid #008069;";
            span.innerHTML = emoji + " " + count;
            display.appendChild(span);
        }
    }
</script>
