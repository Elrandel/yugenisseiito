<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YUGEN RP | Faction de l'Eau</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Noto+Serif+JP:wght@300;400;700&display=swap');

        :root {
            --bg-dark: #010409;
            --water-main: #0077ff;
            --water-light: #4da6ff;
            --water-dark: #003d80;
            --glass-bg: rgba(5, 15, 30, 0.6);
            --glass-border: rgba(0, 119, 255, 0.2);
            --text-light: #e6f2ff;
            --gold: #d4af37;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            font-family: 'Noto Serif JP', serif;
            margin: 0;
            padding: 0;
            background-image: 
                radial-gradient(circle at 20% 40%, rgba(0, 61, 128, 0.4) 0%, transparent 40%),
                radial-gradient(circle at 80% 70%, rgba(0, 119, 255, 0.15) 0%, transparent 40%);
            background-attachment: fixed;
            min-height: 100vh;
        }

        /* Effet de vagues */
        .wave-container {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 150px;
            overflow: hidden;
            z-index: -1;
            opacity: 0.3;
            pointer-events: none;
        }

        .wave {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 200%;
            height: 100px;
            background: url('data:image/svg+xml;utf8,<svg viewBox="0 0 1200 120" xmlns="http://www.w3.org/2000/svg"><path d="M0,0V46.29c47.79,22.2,103.59,32.17,158,28,70.36-5.37,136.33-33.31,206.8-37.5C438.64,32.43,512.34,53.67,583,72.05c69.27,18,138.3,24.88,209.4,13.08,36.15-6,69.85-17.84,104.45-29.34C989.49,25,1113-14.29,1200,52.47V0Z" fill="%230077ff" opacity=".25"/></svg>') repeat-x;
            background-size: 50% 100%;
            animation: moveWave 15s linear infinite;
        }

        @keyframes moveWave {
            0% { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }

        /* Overlay de Connexion */
        #authOverlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(1, 4, 9, 0.95);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .auth-box {
            background: var(--glass-bg);
            border: 1px solid var(--water-main);
            padding: 3rem;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 0 40px rgba(0, 119, 255, 0.4);
            width: 100%;
            max-width: 400px;
        }

        header {
            text-align: center;
            padding: 2.5rem 1rem;
            background: rgba(1, 4, 9, 0.8);
            border-bottom: 1px solid var(--water-main);
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 30px rgba(0, 119, 255, 0.2);
        }

        .yugen-tag {
            font-family: 'Cinzel', serif;
            color: var(--gold);
            font-size: 0.9rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-bottom: 10px;
            display: block;
        }

        h1 {
            font-family: 'Cinzel', serif;
            color: var(--water-light);
            font-size: 2.8rem;
            margin: 0;
            text-shadow: 0 0 15px rgba(0, 119, 255, 0.6);
        }

        .container {
            max-width: 1200px;
            margin: 2rem auto;
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 2rem;
            padding: 0 1rem;
            transition: all 0.5s ease;
        }

        .container.guest-mode {
            grid-template-columns: 1fr;
            max-width: 800px;
        }

        @media (max-width: 850px) {
            .container { grid-template-columns: 1fr; }
        }

        .glass-panel {
            background: var(--glass-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5);
        }

        h2 {
            font-family: 'Cinzel', serif;
            color: var(--water-light);
            border-bottom: 1px solid var(--glass-border);
            padding-bottom: 10px;
            margin-top: 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .form-group { margin-bottom: 15px; }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #99ccff;
            font-size: 0.9rem;
            letter-spacing: 1px;
        }

        input, select, textarea {
            width: 100%;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--glass-border);
            color: var(--text-light);
            padding: 10px 12px;
            font-family: inherit;
            box-sizing: border-box;
            border-radius: 6px;
            transition: all 0.3s ease;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--water-light);
            box-shadow: 0 0 10px rgba(0, 119, 255, 0.3);
            background: rgba(0, 0, 0, 0.6);
        }

        .tools-row {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
            background: rgba(0, 61, 128, 0.2);
            padding: 10px;
            border-radius: 6px;
            border: 1px dashed var(--water-dark);
        }

        .btn-insert {
            background: var(--water-dark);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.2s;
        }

        .btn-insert:hover { background: var(--water-main); }

        textarea { resize: vertical; min-height: 180px; line-height: 1.5; }

        button.submit-btn {
            margin-top: 15px;
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, var(--water-dark), var(--water-main));
            color: #fff;
            border: 1px solid var(--water-light);
            font-family: 'Cinzel', serif;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            border-radius: 6px;
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 4px 15px rgba(0, 119, 255, 0.3);
        }

        button.submit-btn:hover {
            background: linear-gradient(135deg, var(--water-main), var(--water-light));
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 119, 255, 0.5);
        }

        .reports-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            max-height: 800px;
            overflow-y: auto;
            padding-right: 5px;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: rgba(0,0,0,0.2); border-radius: 4px; }
        ::-webkit-scrollbar-thumb { background: var(--water-dark); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--water-main); }

        .report-card {
            background: rgba(0, 0, 0, 0.5);
            border-left: 4px solid var(--water-main);
            padding: 1.5rem;
            border-radius: 6px;
            position: relative;
            transition: all 0.3s ease;
        }

        .report-card:hover {
            border-left-color: var(--water-light);
            background: rgba(5, 15, 30, 0.8);
        }

        .report-header { margin-bottom: 10px; padding-right: 90px; }

        .report-title {
            font-size: 1.3rem;
            color: var(--water-light);
            margin: 0 0 5px 0;
            font-family: 'Cinzel', serif;
        }

        .report-meta { font-size: 0.8rem; color: #6699cc; }
        
        .report-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 15px;
            font-size: 0.85rem;
        }

        .tag {
            background: rgba(0, 119, 255, 0.15);
            padding: 4px 8px;
            border-radius: 4px;
            border: 1px solid rgba(0, 119, 255, 0.3);
            color: #b3d9ff;
        }

        .report-content {
            line-height: 1.6;
            white-space: pre-wrap;
            color: #cce6ff;
            font-size: 0.95rem;
            border-top: 1px dashed var(--glass-border);
            padding-top: 10px;
        }

        /* Styles pour la galerie d'images */
        .report-images {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
            border-top: 1px dashed var(--glass-border);
            padding-top: 15px;
        }

        .report-images img {
            height: 100px;
            width: auto;
            max-width: 100%;
            border-radius: 6px;
            border: 1px solid var(--glass-border);
            object-fit: cover;
            transition: transform 0.3s, border-color 0.3s;
            cursor: pointer;
        }

        .report-images img:hover {
            transform: scale(1.05);
            border-color: var(--water-light);
        }

        .action-buttons {
            position: absolute;
            top: 15px;
            right: 15px;
            display: flex;
            gap: 8px;
        }

        .icon-btn {
            background: rgba(0, 0, 0, 0.5);
            color: var(--water-light);
            width: 35px;
            height: 35px;
            border-radius: 4px;
            font-size: 1.1rem;
            cursor: pointer;
            border: 1px solid var(--glass-border);
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .icon-btn:hover {
            background: var(--water-main);
            color: white;
            border-color: var(--water-light);
        }

        optgroup { background-color: var(--bg-dark); color: var(--water-light); }
        option { background-color: #01060e; color: var(--text-light); }
    </style>
</head>
<body>

    <!-- OVERLAY DE CONNEXION -->
    <div id="authOverlay">
        <h1 style="margin-bottom: 2rem;">Mizu no Kokyū 🌊</h1>
        <div class="auth-box">
            <h2 style="justify-content: center;">🔒 Accès Sécurisé</h2>
            <p style="color: #99ccff; margin-bottom: 20px; font-size: 0.9rem;">Veuillez décliner votre identité.</p>
            
            <input type="password" id="authPassword" placeholder="Mot de passe..." style="text-align: center; margin-bottom: 15px; font-size: 1.2rem; padding: 15px;">
            
            <button class="submit-btn" onclick="checkAuth()" style="margin-top: 0; margin-bottom: 15px;">Déverrouiller</button>
            <button class="btn-insert" onclick="guestLogin()" style="width: 100%; background: transparent; border: 1px solid var(--water-dark); color: var(--water-light);">Mode Invité (Lecture Seule)</button>
        </div>
    </div>

    <div class="wave-container"><div class="wave"></div></div>

    <header>
        <span class="yugen-tag">Serveur Yugen RP</span>
        <h1>Mizu no Kokyū 🌊</h1>
        <div style="font-style: italic; color: #99ccff; margin-top: 5px;">Registre Officiel - Faction de l'Eau</div>
    </header>

    <div class="container" id="mainContainer">
        <!-- FORMULAIRE (Sera caché pour les invités) -->
        <div class="glass-panel" id="formPanel">
            <h2>📜 Nouveau Rapport</h2>
            <form id="reportForm">
                
                <div class="form-group">
                    <label>Nom de l'Opération / Patrouille</label>
                    <input type="text" id="missionName" required placeholder="Ex: Reconnaissance au village de l'Est">
                </div>

                <div class="form-group">
                    <label>Grade Actuel</label>
                    <select id="slayerRank">
                        <optgroup label="Dirigeants">
                            <option value="👑 | Maître des pourfendeurs">👑 | Maître des pourfendeurs</option>
                            <option value="🎆 | Conseiller du Maître">🎆 | Conseiller du Maître</option>
                        </optgroup>
                        <optgroup label="Gérants de souffle">
                            <option value="🏆 | Pilier de l'Eau">🏆 | Pilier de l'Eau</option>
                            <option value="🥇 | Kinoe">🥇 | Kinoe</option>
                        </optgroup>
                        <optgroup label="Hauts Gradés">
                            <option value="🥈 | Kinoto">🥈 | Kinoto</option>
                            <option value="🥉 | Hinoe">🥉 | Hinoe</option>
                        </optgroup>
                        <optgroup label="Gradés">
                            <option value="🎇 | Hinoto">🎇 | Hinoto</option>
                            <option value="⚜️ | Tsuchinoe">⚜️ | Tsuchinoe</option>
                            <option value="🔰 | Tsuchinoto" selected>🔰 | Tsuchinoto</option>
                        </optgroup>
                        <optgroup label="Bas Gradés">
                            <option value="🛡️ | Kanoe">🛡️ | Kanoe</option>
                            <option value="🗡️ | Kanoto">🗡️ | Kanoto</option>
                            <option value="🏹 | Mizunoe">🏹 | Mizunoe</option>
                            <option value="⚔️ | Mizunoto">⚔️ | Mizunoto</option>
                        </optgroup>
                    </select>
                </div>

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <div class="form-group">
                        <label>Zone / Lieu</label>
                        <input type="text" id="location" required placeholder="Forêt, Ville, Montagne...">
                    </div>
                    <div class="form-group">
                        <label>Démons Éliminés</label>
                        <input type="number" id="demonsSlain" min="0" value="0">
                    </div>
                </div>

                <!-- OUTIL GUIDE DES SAVOIRS -->
                <div class="form-group">
                    <label>📖 Guide des Savoirs (Insertion Rapide)</label>
                    <div class="tools-row">
                        <select id="breathingForms" style="flex: 1;">
                            <option value="">-- Sélectionner une posture --</option>
                            <option value="1er Mouvement : Entaille de l'eau en surface (Minamo Giri)">1er Mouv: Entaille de l'eau en surface</option>
                            <option value="2ème Mouvement : Roue d'eau (Mizu Guruma)">2ème Mouv: Roue d'eau</option>
                            <option value="3ème Mouvement : Danse des Courants (Ryūryū Mai)">3ème Mouv: Danse des Courants</option>
                            <option value="4ème Mouvement : Frappe de la Marée (Uchishio)">4ème Mouv: Frappe de la Marée</option>
                            <option value="5ème Mouvement : Averse Miséricordieuse (Kanten no Jiu)">5ème Mouv: Averse Miséricordieuse</option>
                            <option value="6ème Mouvement : Tourbillon (Nejire Uzu)">6ème Mouv: Tourbillon</option>
                            <option value="7ème Mouvement : Goutte de Rosée (Shizuku Hamon Tsuki)">7ème Mouv: Goutte de Rosée</option>
                            <option value="8ème Mouvement : Impact de la Cascade (Takitsubo)">8ème Mouv: Impact de la Cascade</option>
                            <option value="9ème Mouvement : Éclaboussure Chaotique (Suiryū Shibuki)">9ème Mouv: Éclaboussure Chaotique</option>
                            <option value="10ème Mouvement : Le Dragon du Changement (Seisei Ruten)">10ème Mouv: Dragon du Changement</option>
                        </select>
                        <button type="button" class="btn-insert" onclick="insertForm()" title="Insérer dans le texte">➕ Ajouter</button>
                    </div>
                </div>

                <div class="form-group">
                    <label>Récit Détaillé (Déroulement, blessures, alliés présents)</label>
                    <textarea id="details" required placeholder="Rédigez l'historique de la mission ici..."></textarea>
                </div>

                <!-- NOUVELLE SECTION : IMAGES -->
                <div class="form-group">
                    <label>📸 Preuves Visuelles (Liens des images)</label>
                    <input type="text" id="imageUrls" placeholder="Ex: https://i.imgur.com/..., https://cdn.discordapp.com/... (séparées par des virgules)">
                </div>

                <button type="submit" class="submit-btn">Archiver le Rapport</button>
            </form>
        </div>

        <!-- AFFICHAGE -->
        <div class="glass-panel">
            <h2>📁 Archives Yugen</h2>
            <div id="reportsContainer" class="reports-list">
                <!-- Javascript injectera les rapports ici -->
            </div>
        </div>
    </div>

    <script>
        // === SYSTÈME D'AUTHENTIFICATION ===
        let isGuest = false;

        document.getElementById('authPassword').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') {
                checkAuth();
            }
        });

        function checkAuth() {
            const pwd = document.getElementById('authPassword').value;
            if (pwd === "GuizTropBeau") {
                document.getElementById('authOverlay').style.display = 'none';
                isGuest = false;
                renderReports();
            } else {
                alert("❌ Mot de passe incorrect ! Les archives te sont scellées.");
                document.getElementById('authPassword').value = '';
            }
        }

        function guestLogin() {
            document.getElementById('authOverlay').style.display = 'none';
            document.getElementById('formPanel').style.display = 'none';
            document.getElementById('mainContainer').classList.add('guest-mode');
            isGuest = true;
            renderReports();
        }

        // === FONCTION D'INSERTION RAPIDE DU SAVOIR ===
        function insertForm() {
            const formSelect = document.getElementById('breathingForms');
            const textarea = document.getElementById('details');
            const selectedForm = formSelect.value;
            
            if (!selectedForm) return;

            const startPos = textarea.selectionStart;
            const endPos = textarea.selectionEnd;
            const textBefore = textarea.value.substring(0, startPos);
            const textAfter = textarea.value.substring(endPos, textarea.value.length);
            
            textarea.value = textBefore + " [" + selectedForm + "] " + textAfter;
            
            textarea.focus();
            textarea.selectionStart = startPos + selectedForm.length + 4;
            textarea.selectionEnd = startPos + selectedForm.length + 4;
            
            formSelect.value = "";
        }

        // === GESTION DES RAPPORTS ===
        let reports = JSON.parse(localStorage.getItem('yugen_water_reports')) || [];

        const form = document.getElementById('reportForm');
        const container = document.getElementById('reportsContainer');

        function renderReports() {
            container.innerHTML = '';
            
            if (reports.length === 0) {
                container.innerHTML = '<p style="color: #6699cc; font-style: italic; text-align: center; padding: 2rem 0;">Aucune archive trouvée dans les registres.</p>';
                return;
            }

            const reversedReports = [...reports].reverse();

            reversedReports.forEach((report, index) => {
                const originalIndex = reports.length - 1 - index;
                const dateObj = new Date(report.date);
                const dateStr = dateObj.toLocaleDateString('fr-FR') + ' - ' + dateObj.toLocaleTimeString('fr-FR', {hour: '2-digit', minute:'2-digit'});

                const deleteButtonHtml = isGuest ? '' : `<button class="icon-btn" onclick="deleteReport(${originalIndex})" title="Supprimer l'archive" style="color: #ff4d4d;">🗑️</button>`;

                // Gestion de l'affichage des images
                let imagesHtml = '';
                if (report.images && report.images.length > 0) {
                    imagesHtml = '<div class="report-images">';
                    report.images.forEach(imgUrl => {
                        imagesHtml += `<a href="${imgUrl}" target="_blank" title="Cliquez pour agrandir"><img src="${imgUrl}" alt="Preuve Visuelle" onerror="this.style.display='none'"></a>`;
                    });
                    imagesHtml += '</div>';
                }

                const card = document.createElement('div');
                card.className = 'report-card';
                card.innerHTML = `
                    <div class="action-buttons">
                        <button class="icon-btn" onclick="copyReport(${originalIndex})" title="Copier pour Discord">📋</button>
                        ${deleteButtonHtml}
                    </div>
                    <div class="report-header">
                        <h3 class="report-title">${report.name}</h3>
                        <div class="report-meta">📅 ${dateStr}</div>
                    </div>
                    <div class="report-tags">
                        <span class="tag">🎖️ ${report.rank}</span>
                        <span class="tag">📍 ${report.location}</span>
                        <span class="tag">👹 Démons: ${report.kills}</span>
                    </div>
                    <div class="report-content">${report.details}</div>
                    ${imagesHtml}
                `;
                container.appendChild(card);
            });
        }

        form.addEventListener('submit', function(e) {
            e.preventDefault();
            if (isGuest) return;

            // Récupération et traitement des liens d'images
            const rawImageUrls = document.getElementById('imageUrls').value;
            const imagesArray = rawImageUrls ? rawImageUrls.split(',').map(url => url.trim()).filter(url => url !== "") : [];

            const newReport = {
                name: document.getElementById('missionName').value,
                rank: document.getElementById('slayerRank').value,
                location: document.getElementById('location').value,
                kills: document.getElementById('demonsSlain').value,
                details: document.getElementById('details').value,
                images: imagesArray,
                date: new Date().toISOString()
            };

            reports.push(newReport);
            localStorage.setItem('yugen_water_reports', JSON.stringify(reports));
            
            const currentRank = document.getElementById('slayerRank').value;
            form.reset();
            document.getElementById('slayerRank').value = currentRank;
            
            renderReports();
        });

        window.deleteReport = function(index) {
            if (isGuest) return;
            if(confirm("Action irréversible. Supprimer ce rapport officiel ?")) {
                reports.splice(index, 1);
                localStorage.setItem('yugen_water_reports', JSON.stringify(reports));
                renderReports();
            }
        };

        window.copyReport = function(index) {
            const report = reports[index];
            
            // Formatage des images pour Discord
            let discordImagesText = "";
            if (report.images && report.images.length > 0) {
                discordImagesText = "\n\n**[ PREUVES VISUELLES ]**\n" + report.images.join("\n");
            }

            const textToCopy = `━━━━━━━━ 🌊 **ARCHIVE DE FACTION** 🌊 ━━━━━━━━
> **Rapport de :** ${report.name}
> **Grade du Rédacteur :** ${report.rank}
> **Lieu de l'Opération :** ${report.location}
> **Bilan des Éliminations :** ${report.kills} Démon(s)

**[ RÉCIT DES ÉVÉNEMENTS ]**
\`\`\`
${report.details}
\`\`\`${discordImagesText}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━`;

            navigator.clipboard.writeText(textToCopy).then(() => {
                alert("Le format Discord a été copié. Prêt à être collé sur le serveur Yugen !");
            }).catch(err => {
                alert("Erreur lors de la copie du presse-papiers.");
            });
        };
    </script>
</body>
</html>
