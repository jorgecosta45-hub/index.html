<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Agenda Patrimonial - Jorge Costa</title>
    <style>
        /* Reset Estrutural Absoluto - Sem Scroll Lateral */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        body { 
            background-color: #020617; 
            color: #f8fafc; 
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            padding: 8px 8px 40px 8px;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
            width: 100%;
        }

        /* Moldura Compacta Ajustada para o Telemóvel */
        .app-frame { 
            width: 100%;
            max-width: 100%;
            background-color: #0b1329;
            border: 1px solid #1e293b;
            border-radius: 16px;
            padding: 12px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.5);
        }

        header { text-align: center; margin-bottom: 12px; padding-bottom: 8px; border-bottom: 1px solid #1e293b; }
        h1 { color: #f59e0b; font-size: 18px; font-weight: 800; }
        .owner-zone { margin-top: 4px; display: inline-block; }
        .owner-name { color: #38bdf8; font-size: 12px; font-weight: 700; border-bottom: 1px dashed #38bdf8; cursor: pointer; padding: 2px 6px; }
        p.subtitle { color: #94a3b8; font-size: 11px; margin-top: 2px; }
        
        .section-card { 
            background-color: #111a36; 
            border: 1px solid #1e293b; 
            border-radius: 12px; 
            padding: 12px; 
            margin-bottom: 12px;
            width: 100%;
        }

        h2 { font-size: 13px; margin-bottom: 10px; color: #e2e8f0; }
        
        .form-vertical { display: flex; flex-direction: column; gap: 10px; width: 100%; }
        .form-row { display: flex; flex-direction: column; width: 100%; }
        
        label { display: block; font-size: 10px; font-weight: 700; color: #94a3b8; text-transform: uppercase; margin-bottom: 4px; }
        
        input, select { 
            width: 100%; 
            background-color: #070d1e; 
            border: 1px solid #273556; 
            border-radius: 6px; 
            padding: 8px 10px; 
            color: white; 
            font-size: 13px; 
            font-weight: 600;
            outline: none;
            height: 40px;
            -webkit-appearance: none;
        }
        input:focus, select:focus { border-color: #f59e0b; }
        
        .btn-submit { 
            width: 100%; 
            background: linear-gradient(to right, #059669, #0d9488); 
            color: white; 
            border: none; 
            border-radius: 8px; 
            padding: 12px; 
            font-size: 13px; 
            font-weight: 700; 
            cursor: pointer;
            margin-top: 4px;
            transition: background 0.2s;
        }

        .btn-edit-mode {
            background: linear-gradient(to right, #2563eb, #1d4ed8) !important;
        }
        
        .widgets-grid { display: grid; grid-template-cols: 1fr 1fr; gap: 8px; margin-bottom: 12px; }
        .widget { background-color: #111a36; border: 1px solid #1e293b; padding: 10px; border-radius: 10px; text-align: center; }
        .widget p:first-child { font-size: 9px; text-transform: uppercase; color: #94a3b8; font-weight: 600; }
        .widget p:last-child { font-size: 15px; font-weight: 700; margin-top: 2px; font-family: monospace; }
        
        .pm-highlight { 
            grid-column: span 2; 
            border-color: rgba(16, 185, 129, 0.4); 
            background: linear-gradient(to bottom, #111a36, #022c22/20); 
        }
        
        .table-container { background-color: #111a36; border: 1px solid #1e293b; border-radius: 10px; overflow: hidden; width: 100%; }
        .table-header { padding: 8px 10px; background-color: #0d1527; border-bottom: 1px solid #1e293b; display: flex; justify-content: space-between; align-items: center; }
        .table-wrapper { overflow-x: auto; width: 100%; -webkit-overflow-scrolling: touch; }
        
        table { width: 100%; border-collapse: collapse; text-align: left; font-size: 11px; font-family: monospace; min-width: 560px; }
        th { background-color: #070d1e; padding: 8px; color: #94a3b8; font-weight: 600; text-transform: uppercase; font-size: 9px; }
        td { padding: 8px; border-bottom: 1px solid #1e293b; color: #e2e8f0; }
        
        .badge { padding: 2px 4px; border-radius: 4px; font-size: 9px; font-weight: 700; }
        .badge-put { background-color: rgba(168, 85, 247, 0.15); color: #c084fc; border: 1px solid rgba(168, 85, 247, 0.3); }
        .badge-call { background-color: rgba(234, 179, 8, 0.15); color: #facc15; border: 1px solid rgba(234, 179, 8, 0.3); }
        .badge-acao { background-color: rgba(59, 130, 246, 0.15); color: #60a5fa; border: 1px solid rgba(59, 130, 246, 0.3); }
        
        .text-green { color: #34d399 !important; font-weight: 700; }
        .text-red { color: #f87171 !important; }
        .text-blue { color: #38bdf8 !important; font-weight: 700; }
        .text-amber { color: #fbbf24 !important; }
        
        .clear-btn { font-size: 10px; color: #f87171; background: none; border: none; text-decoration: underline; cursor: pointer; }
        
        .btn-action { background: none; border: none; font-weight: 700; font-size: 10px; cursor: pointer; margin: 0 2px; padding: 2px 4px; }
        .btn-edit { color: #38bdf8; }
        .btn-delete { color: #f87171; }

        .backup-container { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; padding-top: 8px; border-top: 1px dashed #1e293b; }
        .btn-backup { flex: 1; min-width: 100px; background-color: #1e293b; color: #cbd5e1; border: 1px solid #334155; border-radius: 6px; padding: 10px 6px; font-size: 11px; font-weight: 700; cursor: pointer; text-align: center; -webkit-appearance: none; }
        .btn-print { background-color: #0d9488; color: white; border-color: #14b8a6; }

        #zonaExportacao { display: none; margin-top: 10px; background-color: #070d1e; border: 1px solid #f59e0b; padding: 10px; border-radius: 8px; }
        #txtBackup { width: 100%; height: 80px; background-color: #020617; color: #34d399; font-family: monospace; font-size: 10px; padding: 5px; border: 1px solid #1e293b; border-radius: 4px; margin-bottom: 6px; }

        footer {
            width: 100%;
            text-align: center;
            font-size: 10px;
            color: #475569;
            padding: 12px 0;
            margin-top: 16px;
            border-top: 1px solid #1e293b;
            font-weight: 500;
        }

        @media print {
            body { background: white !important; color: black !important; padding: 0 !important; }
            .app-frame { border: none !important; box-shadow: none !important; background: transparent !important; }
            header, .section-card:nth-of-type(1), .backup-container, .widgets-grid, footer, .col-acao, .clear-btn { display: none !important; }
            .section-card:nth-of-type(2) { background: transparent !important; border: none !important; padding: 0 !important; }
            #zonaTabelaImpressao { border: none !important; background: transparent !important; }
            table { min-width: 100% !important; color: black !important; }
            th { background: #f1f5f9 !important; color: black !important; border-bottom: 2px solid black !important; }
            td { color: black !important; border-bottom: 1px solid #e2e8f0 !important; }
            .text-green, .text-blue, .text-amber { color: black !important; }
            .badge { border: 1px solid #000 !important; color: #000 !important; background: transparent !important; }
        }
    </style>
</head>
<body>

    <div class="app-frame">
        <header>
            <h1>📈 AGENDA PATRIMONIAL</h1>
            <div class="owner-zone">
                <span class="owner-name" id="nomeProprietario" onclick="alterarNomeDono()">CLIQUE PARA DEFINIR O PROPRIETÁRIO</span>
            </div>
            <p class="subtitle">Controlo de PM, Rolagens e Posições da Carteira</p>
        </header>

        <div class="section-card">
            <h2 id="tituloFormulario">✍️ Registar Movimento</h2>
            <form id="agendaForm" class="form-vertical">
                <div class="form-row">
                    <label>Ativo (Ticker)</label>
                    <input type="text" id="ativo" placeholder="Ex: SABR" required style="text-transform: uppercase; font-weight: 700; color: #fbbf24;">
                </div>
                <div class="form-row">
                    <label>Data Op.</label>
                    <input type="date" id="dataOp" required>
                </div>
                <div class="form-row">
                    <label>Instrumento</label>
                    <select id="instrumento" onchange="toggleOptionFields()">
                        <option value="OPCAO">OPÇÃO</option>
                        <option value="ACAO">AÇÃO</option>
                    </select>
                </div>
                <div class="form-row" id="containerCallPut">
                    <label>Tipo Opção</label>
                    <select id="tipoOpcao" onchange="ajustarLabelsDinamicos()">
                        <option value="PUT">PUT</option>
                        <option value="CALL">CALL</option>
                    </select>
                </div>
                <div class="form-row">
                    <label>Direção</label>
                    <select id="direcao" onchange="ajustarLabelsDinamicos()">
                        <option value="VENDA">VENDA (Recebe Prémio)</option>
                        <option value="COMPRA">COMPRA (Aloca Capital / Ações)</option>
                    </select>
                </div>
                <div class="form-row" id="containerPrecoAtivo">
                    <label id="labelPrecoRef">Preço Ref. Strike ($)</label>
                    <input type="number" step="0.001" id="precoAtivo" placeholder="0.00">
                </div>
                <div class="form-row">
                    <label id="labelQtd">Quantidade (Ações)</label>
                    <input type="number" id="qtdAcoes" placeholder="100">
                </div>
                <div class="form-row">
                    <label id="labelFinanceiro">Prémio Recebido / Pago ($)</label>
                    <input type="number" step="0.01" id="valorFinanceiro" placeholder="0.00" style="font-weight: 700; color: #34d399;">
                </div>
                <button type="submit" id="btnSubmitForm" class="btn-submit">Gravar na Agenda</button>
            </form>
        </div>

        <div class="section-card" style="padding: 10px;">
            <div style="display: flex; justify-content: space-between; align-items: center; gap: 8px;">
                <div style="flex-grow: 1;">
                    <label>🔍 Filtrar por Ativo</label>
                    <select id="filtroAtivo" style="color: #fbbf24; font-weight: 700; height: 36px; font-size: 12px;"></select>
                </div>
                <div style="margin-top: 12px;">
                    <button onclick="limparTudo()" class="clear-btn">Limpar Tudo</button>
                </div>
            </div>
            
            <div class="backup-container">
                <button onclick="exportarBackupMobile()" class="btn-backup">📥 Exportar</button>
                <button onclick="importarBackup()" class="btn-backup">📤 Importar</button>
                <button onclick="imprimirSeguro()" class="btn-backup btn-print">🖨️ Imprimir Histórico</button>
                <input type="file" id="fileInput" style="display: none;" accept=".json" onchange="processarArquivoBackup(event)">
            </div>

            <div id="zonaExportacao">
                <label style="color: #fbbf24;">Código de Segurança Gerado:</label>
                <textarea id="txtBackup" readonly onclick="this.select()"></textarea>
                <button onclick="copiarTextoBackup()" class="btn-submit" style="padding: 6px; font-size: 11px; background: #2563eb;">📋 Copiar Código</button>
            </div>
        </div>

        <div class="widgets-grid">
            <div class="widget">
                <p>Capital Alocado</p>
                <p id="resumoTotalAplicado" style="color: white;">$0.00</p>
            </div>
            <div class="widget">
                <p>Ações Detidas</p>
                <p id="resumoTotalAcoes" style="color: #fbbf24;">0</p>
            </div>
            <div class="widget pm-highlight">
                <p style="color: #34d399 !important;">Preço Médio Real (PM)</p>
                <p id="resumoPM" style="color: #34d399;">$0.000</p>
            </div>
        </div>

        <div class="table-container" id="zonaTabelaImpressao">
            <div class="table-header">
                <span style="font-size: 10px; font-weight: 700; text-transform: uppercase; color: #94a3b8;">Histórico</span>
                <span id="badgeAtivo" style="background-color: rgba(245,158,11,0.1); color: #f59e0b; padding: 1px 6px; border-radius: 4px; font-size: 9px; font-weight: 700;">TODOS</span>
            </div>
            <div class="table-wrapper">
                <table id="tabelaReal">
                    <thead>
                        <tr>
                            <th style="padding-left: 8px;">Data</th>
                            <th>Ativo</th>
                            <th>Inst.</th>
                            <th>Dir.</th>
                            <th>Ref.</th>
                            <th>Qtd</th>
                            <th>Fluxo</th>
                            <th style="color: #fbbf24;">Acum.</th>
                            <th style="color: #34d399;">PM Real</th>
                            <th class="col-acao" style="text-align: center; color: #a1a1aa;">Ações</th>
                        </tr>
                    </thead>
                    <tbody id="tabelaCorpo"></tbody>
                </table>
            </div>
        </div>

        <footer>
            © 2026 · <span id="footerNome">Agenda Patrimonial</span> · Todos os direitos reservados
        </footer>
    </div>

    <script>
        let agenda = JSON.parse(localStorage.getItem('agenda_operacional_data')) || [];
        let idItemEditando = null; 

        function carregarNomeProprietario() {
            const nomeSalvo = localStorage.getItem('agenda_owner_name');
            const elementoCabecalho = document.getElementById('nomeProprietario');
            const elementoFooter = document.getElementById('footerNome');
            if (nomeSalvo && nomeSalvo.trim() !== "") {
                elementoCabecalho.innerText = nomeSalvo;
                elementoFooter.innerText = nomeSalvo;
            }
        }

        function alterarNomeDono() {
            const nomeAtual = localStorage.getItem('agenda_owner_name') || "";
            const novoNome = prompt("Digite o nome do Proprietário da Agenda:", nomeAtual);
            if (novoNome !== null) {
                localStorage.setItem('agenda_owner_name', novoNome.trim());
                carregarNomeProprietario();
            }
        }

        function toggleOptionFields() {
            const inst = document.getElementById('instrumento').value;
            const containerCallPut = document.getElementById('containerCallPut');
            const selectOpcao = document.getElementById('tipoOpcao');
            if(inst === 'ACAO') {
                containerCallPut.style.display = 'none';
                selectOpcao.disabled = true;
                if(idItemEditando === null) document.getElementById('direcao').value = 'COMPRA';
            } else {
                containerCallPut.style.display = 'flex';
                selectOpcao.disabled = false;
                if(idItemEditando === null) document.getElementById('direcao').value = 'VENDA';
            }
            ajustarLabelsDinamicos();
        }

        function ajustarLabelsDinamicos() {
            const inst = document.getElementById('instrumento').value;
            const dir = document.getElementById('direcao').value;
            const tipoOp = document.getElementById('tipoOpcao').value;
            const labelFin = document.getElementById('labelFinanceiro');
            const inputFin = document.getElementById('valorFinanceiro');
            const labelPreco = document.getElementById('labelPrecoRef');

            if (inst === 'ACAO') {
                labelPreco.innerText = "Preço da Ação ($)";
                labelFin.innerText = "Fluxo Financeiro Total ($)";
                inputFin.style.color = "#f8fafc";
            } else {
                if (tipoOp === 'PUT') {
                    labelFin.innerText = "Prémio Recebido / Pago ($)";
                } else {
                    labelFin.innerText = "Fluxo Financeiro Total ($)";
                }
                labelPreco.innerText = "Preço Ref. Strike ($)";
                if (dir === 'VENDA') {
                    inputFin.style.color = "#34d399";
                } else {
                    inputFin.style.color = "#f87171";
                }
            }
        }

        document.getElementById('agendaForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const ticker = document.getElementById('ativo').value.toUpperCase().trim();
            const dataRaw = document.getElementById('dataOp').value;
            const dataFormatada = dataRaw.split('-').reverse().join('/');
            const direcao = document.getElementById('direcao').value;
            const instrumento = document.getElementById('instrumento').value;
            const tipoOpcao = instrumento === 'OPCAO' ? document.getElementById('tipoOpcao').value : 'N/A';
            const preco = parseFloat(document.getElementById('precoAtivo').value) || 0;
            const qtd = parseInt(document.getElementById('qtdAcoes').value) || 0;
            const valorBruto = parseFloat(document.getElementById('valorFinanceiro').value) || 0;

            let valorEfeito = 0; let qtdEfeito = 0;
            if (instrumento === 'OPCAO') {
                valorEfeito = (direcao === 'VENDA') ? -valorBruto : valorBruto;
                qtdEfeito = 0; 
            } else { 
                if (direcao === 'COMPRA') { valorEfeito = valorBruto; qtdEfeito = qtd; } 
                else { valorEfeito = -valorBruto; qtdEfeito = -qtd; }
            }

            if (idItemEditando !== null) {
                const index = agenda.findIndex(item => item.id === idItemEditando);
                if (index !== -1) {
                    agenda[index].ticker = ticker; agenda[index].data = dataFormatada;
                    agenda[index].direcao = direcao; agenda[index].instrumento = instrumento;
                    agenda[index].tipoOpcao = tipoOpcao; agenda[index].preco = preco;
                    agenda[index].qtdOriginal = qtd; agenda[index].qtdEfeito = qtdEfeito;
                    agenda[index].valorEfeito = valorEfeito;
                }
                idItemEditando = null;
                const btnSubmit = document.getElementById('btnSubmitForm');
                btnSubmit.innerText = "Gravar na Agenda";
                btnSubmit.classList.remove('btn-edit-mode');
                document.getElementById('tituloFormulario').innerText = "✍️ Registar Movimento";
            } else {
                const idUnico = Date.now() + Math.floor(Math.random() * 1000);
                agenda.push({ id: idUnico, ticker, data: dataFormatada, direcao, instrumento, tipoOpcao, preco, qtdOriginal: qtd, qtdEfeito, valorEfeito });
            }
            localStorage.setItem('agenda_operacional_data', JSON.stringify(agenda));
            document.getElementById('zonaExportacao').style.display = 'none';
            atualizarListaFiltros(); processarAgenda(); document.getElementById('agendaForm').reset(); toggleOptionFields();
        });

        function prepararEdicao(idUnico) {
            const item = agenda.find(op => op.id === idUnico);
            if (!item) return;
            idItemEditando = item.id;
            const partesData = item.data.split('/');
            if(partesData.length === 3) document.getElementById('dataOp').value = `${partesData[2]}-${partesData[1]}-${partesData[0]}`;
            document.getElementById('ativo').value = item.ticker;
            document.getElementById('instrumento').value = item.instrumento;
            toggleOptionFields();
            if (item.instrumento === 'OPCAO') document.getElementById('tipoOpcao').value = item.tipoOpcao;
            document.getElementById('direcao').value = item.direcao;
            document.getElementById('precoAtivo').value = item.preco;
            document.getElementById('qtdAcoes').value = item.qtdOriginal;
            document.getElementById('valorFinanceiro').value = Math.abs(item.valorEfeito);
            ajustarLabelsDinamicos();
            document.getElementById('tituloFormulario').innerText = "✏️ Modo de Edição Ativo";
            const btnSubmit = document.getElementById('btnSubmitForm');
            btnSubmit.innerText = "Atualizar Movimento"; btnSubmit.classList.add('btn-edit-mode');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function excluirItem(idUnico) {
            if(confirm('Tem a certeza que deseja eliminar esta operação do histórico?')) {
                agenda = agenda.filter(item => item.id !== idUnico);
                localStorage.setItem('agenda_operacional_data', JSON.stringify(agenda));
                if(idItemEditando === idUnico) {
                    idItemEditando = null; document.getElementById('agendaForm').reset();
                    const btnSubmit = document.getElementById('btnSubmitForm');
                    btnSubmit.innerText = "Gravar na Agenda"; btnSubmit.classList.remove('btn-edit-mode');
                    document.getElementById('tituloFormulario').innerText = "✍️ Registar Movimento"; toggleOptionFields();
                }
                document.getElementById('zonaExportacao').style.display = 'none';
                atualizarListaFiltros(); processarAgenda();
            }
        }

        function atualizarListaFiltros(forçarSelecionado = '') {
            const seletor = document.getElementById('filtroAtivo');
            const ativoAnterior = forçarSelecionado || seletor.value || 'TODOS';
            let tickers = ['TODOS', ...new Set(agenda.map(item => item.ticker))];
            seletor.innerHTML = '';
            tickers.forEach(t => {
                const opt = document.createElement('option');
                opt.value = t; opt.innerText = t;
                if(t === ativoAnterior) opt.selected = true;
                seletor.appendChild(opt);
            });
        }

        document.getElementById('filtroAtivo').addEventListener('change', processarAgenda);

        function processarAgenda() {
            const filtro = document.getElementById('filtroAtivo').value || 'TODOS';
            document.getElementById('badgeAtivo').innerText = filtro;
            const corpo = document.getElementById('tabelaCorpo');
            corpo.innerHTML = '';

            let dineroPorAtivo = {}; let acoesPorAtivo = {};

            agenda.forEach(op => {
                const t = op.ticker;
                if (!dineroPorAtivo[t]) { dineroPorAtivo[t] = 0; acoesPorAtivo[t] = 0; }
                dineroPorAtivo[t] += op.valorEfeito; acoesPorAtivo[t] += op.qtdEfeito;

                let pmEvolutivoAtivo = acoesPorAtivo[t] > 0 ? (dineroPorAtivo[t] / acoesPorAtivo[t]) : 0;
                if (filtro === 'TODOS' || t === filtro) {
                    const corValor = op.valorEfeito < 0 ? 'text-green' : '';
                    const sinalPreco = op.valorEfeito < 0 ? '+' : '-';
                    let badgeCls = op.instrumento === 'ACAO' ? 'badge-acao' : (op.tipoOpcao === 'PUT' ? 'badge-put' : 'badge-call');
                    let badgeTxt = op.instrumento === 'ACAO' ? 'AÇÃO' : op.tipoOpcao;
                    let dirTxt = op.direcao === 'VENDA' ? '<span class="text-green">VD</span>' : '<span class="text-blue">CP</span>';

                    corpo.innerHTML += `
                        <tr>
                            <td style="padding-left: 8px; color: #64748b;">${op.data.substring(0,5)}</td>
                            <td class="text-amber"><b>${op.ticker}</b></td>
                            <td><span class="badge ${badgeCls}">${badgeTxt}</span></td>
                            <td>${dirTxt}</td>
                            <td>$${op.preco.toFixed(2)}</td>
                            <td>${op.qtdOriginal}</td>
                            <td class="${corValor}">${sinalPreco}$${Math.abs(op.valorEfeito).toFixed(2)}</td>
                            <td style="color: ${acoesPorAtivo[t] > 0 ? '#fbbf24' : '#64748b'}; font-weight: 600;">${acoesPorAtivo[t]}</td>
                            <td class="text-green" style="font-weight:700;">$${pmEvolutivoAtivo.toFixed(3)}</td>
                            <td class="col-acao" style="text-align: center; white-space: nowrap;">
                                <button onclick="prepararEdicao(${op.id})" class="btn-action btn-edit">Editar</button>
                                <button onclick="excluirItem(${op.id})" class="btn-action btn-delete">X</button>
                            </td>
                        </tr>`;
                }
            });

            if (filtro === 'TODOS') {
                let totalDinheiroExibir = 0; let totalAcoesExibir = 0;
                Object.keys(dineroPorAtivo).forEach(key => { totalDinheiroExibir += dineroPorAtivo[key]; totalAcoesExibir += acoesPorAtivo[key]; });
                document.getElementById('resumoTotalAplicado').innerText = `$${Math.max(0, totalDinheiroExibir).toFixed(2)}`;
                document.getElementById('resumoTotalAcoes').innerText = totalAcoesExibir;
                document.getElementById('resumoPM').innerText = "Múltiplos Ativos"; document.getElementById('resumoPM').style.color = "#94a3b8";
            } else {
                let totalDinheiroExibir = dineroPorAtivo[filtro] || 0; let totalAcoesExibir = acoesPorAtivo[filtro] || 0;
                let pmFinalIsolado = totalAcoesExibir > 0 ? (totalDinheiroExibir / totalAcoesExibir) : 0;
                document.getElementById('resumoTotalAplicado').innerText = `$${Math.max(0, totalDinheiroExibir).toFixed(2)}`;
                document.getElementById('resumoTotalAcoes').innerText = totalAcoesExibir;
                document.getElementById('resumoPM').innerText = `$${pmFinalIsolado.toFixed(3)}`; document.getElementById('resumoPM').style.color = "#34d399";
            }
        }

        function exportarBackupMobile() {
            if(agenda.length === 0) { alert('Não existem dados registados para exportar.'); return; }
            const container = document.getElementById('zonaExportacao');
            if (container.style.display === 'block') { container.style.display = 'none'; } 
            else {
                const jsonString = JSON.stringify(agenda);
                const campoTexto = document.getElementById('txtBackup');
                campoTexto.value = jsonString; container.style.display = 'block'; campoTexto.select();
                window.scrollTo({ top: container.offsetTop, behavior: 'smooth' });
            }
        }

        function copiarTextoBackup() {
            const campoTexto = document.getElementById('txtBackup'); campoTexto.select(); campoTexto.setSelectionRange(0, 99999); 
            try { navigator.clipboard.writeText(campoTexto.value); alert('Código copiado!'); document.getElementById('zonaExportacao').style.display = 'none'; } 
            catch (err) { alert('Pressione e copie manualmente.'); }
        }

        function importarBackup() { document.getElementById('fileInput').click(); }
        function processarArquivoBackup(event) {
            const arquivo = event.target.files[0]; if (!arquivo) return;
            const leitor = new FileReader();
            leitor.onload = function(e) {
                try {
                    const dadosImportados = JSON.parse(e.target.result);
                    if (Array.isArray(dadosImportados)) {
                        if(confirm('Aviso: O histórico será substituído. Continuar?')) {
                            agenda = dadosImportados; agenda.forEach(item => { if(!item.id) item.id = Date.now() + Math.floor(Math.random() * 1000); });
                            localStorage.setItem('agenda_operacional_data', JSON.stringify(agenda));
                            idItemEditando = null; document.getElementById('zonaExportacao').style.display = 'none';
                            atualizarListaFiltros('TODOS'); processarAgenda(); alert('Restaurado!');
                        }
                    } else { alert('Erro: Conteúdo inválido.'); }
                } catch (err) { alert('Erro ao ler o ficheiro.'); }
            };
            leitor.readAsText(arquivo);
        }

        function imprimirSeguro() { if(agenda.length === 0) { alert('Não há dados para imprimir.'); return; } window.print(); }
        function limparTudo() {
            if(confirm('Apagar permanentemente todo o histórico?')) {
                if(confirm('Confirmação final: Eliminar tudo?')) {
                    agenda = []; idItemEditando = null; localStorage.setItem('agenda_operacional_data', JSON.stringify(agenda));
                    document.getElementById('zonaExportacao').style.display = 'none'; atualizarListaFiltros('TODOS'); processarAgenda();
                }
            }
        }

        let alterouLegado = false;
        agenda.forEach(item => { if (!item.id) { item.id = Date.now() + Math.floor(Math.random() * 1000); alterouLegado = true; } });
        if(alterouLegado) localStorage.setItem('agenda_operacional_data', JSON.stringify(agenda));

        carregarNomeProprietario(); atualizarListaFiltros('TODOS'); processarAgenda(); toggleOptionFields();
    </script>
</body>
</html>

