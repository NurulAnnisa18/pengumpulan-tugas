<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manajemen Tugas Kuliah</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            font-size: 2em;
        }

        .input-container {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 30px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            color: #2c3e50;
            font-weight: 600;
        }

        input[type="text"],
        input[type="date"],
        input[type="number"],
        textarea,
        select {
            width: 100%;
            padding: 10px;
            border: 2px solid #e0e0e0;
            border-radius: 5px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        input:focus,
        textarea:focus,
        select:focus {
            border-color: #3498db;
            outline: none;
        }

        .date-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 15px;
        }

        .date-group {
            display: flex;
            flex-direction: column;
        }

        button {
            background-color: #3498db;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
            font-weight: 600;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #2980b9;
        }

        .task-list {
            list-style: none;
        }

        .task-item {
            background: white;
            margin-bottom: 15px;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            border-left: 5px solid #3498db;
        }

        .task-header {
            display: flex;
            align-items: flex-start;
            gap: 15px;
            margin-bottom: 15px;
        }

        .task-info {
            flex-grow: 1;
            line-height: 1.6;
        }

        .task-info.completed {
            text-decoration: line-through;
            color: #7f8c8d;
        }

        .delete-btn {
            background-color: #e74c3c;
            padding: 8px 15px;
            width: auto;
        }

        .delete-btn:hover {
            background-color: #c0392b;
        }

        .progress-container {
            margin: 10px 0;
        }

        progress {
            width: 100%;
            height: 20px;
            border-radius: 10px;
            overflow: hidden;
        }

        progress::-webkit-progress-bar {
            background-color: #f0f0f0;
            border-radius: 10px;
        }

        progress::-webkit-progress-value {
            background-color: #2ecc71;
            border-radius: 10px;
        }

        @media (max-width: 600px) {
            .date-container {
                grid-template-columns: 1fr;
                gap: 10px;
            }

            .container {
                padding: 15px;
            }

            .task-header {
                flex-direction: column;
            }

            .delete-btn {
                width: 100%;
                margin-top: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Manajemen Tugas Kuliah</h1>
        
        <div class="input-container">
            <div class="input-group">
                <label>Nama Tugas:</label>
                <input type="text" id="taskInput" placeholder="Masukkan nama tugas">
            </div>
            
            <div class="date-container">
                <div class="date-group">
                    <label>Tanggal Diberikan:</label>
                    <input type="date" id="assignedDateInput">
                </div>
                <div class="date-group">
                    <label>Deadline:</label>
                    <input type="date" id="deadlineInput">
                </div>
            </div>

            <div class="input-group">
                <label>Progress:</label>
                <input type="number" id="progressInput" min="0" max="100" placeholder="Progress (0-100%)">
            </div>

            <div class="input-group">
                <label>Catatan:</label>
                <textarea id="notesInput" rows="3" placeholder="Catatan progres tugas"></textarea>
            </div>

            <div class="input-group">
                <label>Bukti Pengerjaan:</label>
                <input type="file" id="proofInput" accept="image/*,.pdf,.doc,.docx">
            </div>

            <div class="input-group">
                <label>Pengingat:</label>
                <select id="reminderInput">
                    <option value="">Pilih Pengingat</option>
                    <option value="1">1 hari sebelum deadline</option>
                    <option value="2">2 hari sebelum deadline</option>
                    <option value="3">3 hari sebelum deadline</option>
                    <option value="7">1 minggu sebelum deadline</option>
                </select>
            </div>

            <button onclick="addTask()">Tambah Tugas</button>
        </div>

        <ul class="task-list" id="taskList"></ul>
    </div>

    <script>
        let tasks = [];

        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const assignedDateInput = document.getElementById('assignedDateInput');
            const deadlineInput = document.getElementById('deadlineInput');
            const progressInput = document.getElementById('progressInput');
            const notesInput = document.getElementById('notesInput');
            const proofInput = document.getElementById('proofInput');
            const reminderInput = document.getElementById('reminderInput');

            if (!taskInput.value || !assignedDateInput.value || !deadlineInput.value || !progressInput.value) {
                alert('Mohon isi semua field yang diperlukan!');
                return;
            }

            const task = {
                id: Date.now(),
                name: taskInput.value,
                assignedDate: assignedDateInput.value,
                deadline: deadlineInput.value,
                progress: progressInput.value,
                notes: notesInput.value,
                reminder: reminderInput.value,
                completed: false
            };

            if (proofInput.files.length > 0) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    task.proof = e.target.result;
                    tasks.push(task);
                    saveTasks();
                    loadTasks();
                    clearInputs();
                };
                reader.readAsDataURL(proofInput.files[0]);
            } else {
                tasks.push(task);
                saveTasks();
                loadTasks();
                clearInputs();
            }
        }

        function clearInputs() {
            document.getElementById('taskInput').value = '';
            document.getElementById('assignedDateInput').value = '';
            document.getElementById('deadlineInput').value = '';
            document.getElementById('progressInput').value = '';
            document.getElementById('notesInput').value = '';
            document.getElementById('proofInput').value = '';
            document.getElementById('reminderInput').value = '';
        }

        function deleteTask(id) {
            tasks = tasks.filter(task => task.id !== id);
            saveTasks();
            loadTasks();
        }

        function toggleTask(id) {
            const task = tasks.find(task => task.id === id);
            if (task) {
                task.completed = !task.completed;
                saveTasks();
                loadTasks();
            }
        }

        function saveTasks() {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }

        function loadTasks() {
            tasks = JSON.parse(localStorage.getItem('tasks') || '[]');
            const taskList = document.getElementById('taskList');
            taskList.innerHTML = '';
            
            tasks.forEach(task => {
                const li = document.createElement('li');
                li.className = 'task-item';
                
                const taskHeader = document.createElement('div');
                taskHeader.className = 'task-header';
                
                const checkbox = document.createElement('input');
                checkbox.type = 'checkbox';
                checkbox.checked = task.completed;
                checkbox.onclick = () => toggleTask(task.id);

                const taskInfo = document.createElement('div');
                taskInfo.className = `task-info ${task.completed ? 'completed' : ''}`;
                
                const assignedDate = new Date(task.assignedDate);
                const deadline = new Date(task.deadline);
                const dateDiff = Math.ceil((deadline - assignedDate) / (1000 * 60 * 60 * 24));

                taskInfo.innerHTML = `
                    <strong>${task.name}</strong><br>
                    <span style="color: #3498db">📅 Diberikan: ${assignedDate.toLocaleDateString('id-ID', {
                        weekday: 'long',
                        year: 'numeric',
                        month: 'long',
                        day: 'numeric'
                    })}</span><br>
                    <span style="color: #e74c3c">⏰ Deadline: ${deadline.toLocaleDateString('id-ID', {
                        weekday: 'long',
                        year: 'numeric',
                        month: 'long',
                        day: 'numeric'
                    })}</span><br>
                    <span style="color: #27ae60">⌛ Durasi: ${dateDiff} hari</span>
                `;

                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-btn';
                deleteBtn.innerHTML = '❌ Hapus';
                deleteBtn.onclick = () => deleteTask(task.id);

                taskHeader.appendChild(checkbox);
                taskHeader.appendChild(taskInfo);
                taskHeader.appendChild(deleteBtn);

                const taskDetails = document.createElement('div');
                taskDetails.className = 'task-details';
                
                const now = new Date();
                const daysLeft = Math.ceil((deadline - now) / (1000 * 60 * 60 * 24));
                const timeStatus = daysLeft > 0 
                    ? `<span style="color: #27ae60">Sisa waktu: ${daysLeft} hari</span>`
                    : `<span style="color: #e74c3c">Lewat deadline: ${Math.abs(daysLeft)} hari</span>`;

                taskDetails.innerHTML = `
                    <div class="progress-container">
                        Progress: ${task.progress}%
                        <progress value="${task.progress}" max="100"></progress>
                    </div>
                    <p>${timeStatus}</p>
                    ${task.notes ? `<p>📝 Catatan: ${task.notes}</p>` : ''}
                    ${task.proof ? `<p>📎 Bukti: <img src="${task.proof}" style="max-width: 200px; display: block; margin-top: 10px;"></p>` : ''}
                    ${task.reminder ? `<p>🔔 Pengingat: ${task.reminder} hari sebelum deadline</p>` : ''}
                `;

                li.appendChild(taskHeader);
                li.appendChild(taskDetails);
                taskList.appendChild(li);
            });
        }

        // Load tasks when page loads
        loadTasks();
    </script>
</body>
</html>
