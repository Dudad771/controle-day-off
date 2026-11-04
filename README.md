**Idiomas / Languages:** [Português](#controle-de-day-off) | [English](#day-off-tracker-english-version)

---

# Controle de Day Off

Painel em Excel e script em Google Apps Script que identifica quais colaboradores têm direito a um dia de descanso (day off) no aniversário, após completar 1 ano de empresa, e avisa por e-mail quando o aniversário está chegando.

> **Todos os dados deste repositório são fictícios.** A versão original foi criada em um estágio e não foi publicada por conter dados pessoais (LGPD).

## Prévia

!![E-mail de aviso](email-exemplo.png)

## O problema

O controle do day off de aniversário era feito à mão. Era preciso conferir a data de nascimento e a data de admissão de cada pessoa para saber quem tinha direito ao benefício e quando.

## Como funciona

**Regra:** a pessoa tem direito ao day off se, na data do próximo aniversário, já tiver completado 1 ano de empresa.

**Planilha (Excel / Google Planilhas)**
- **Planilha1:** base de dados com nome, nascimento e admissão. Calcula tempo de casa, próximo aniversário, dias restantes, se tem day off e um alerta para os próximos 30 dias.
- **Painel:** tela de consulta. Escolha um promotor na lista e veja os dados e uma mensagem de aviso (por exemplo, "HOJE é aniversário de ...: utilizar day off!").

**Script (Google Apps Script)**
- Lê a Planilha1 e calcula quem faz aniversário hoje ou nos próximos dias.
- Considera apenas quem terá 1 ano de empresa na data do aniversário.
- Envia um e-mail de aviso, e só envia quando há alguém para avisar.
- Roda todo dia automaticamente, por volta das 8h, por meio de um gatilho.

## Tecnologias

- Excel e Google Planilhas: `DATADIF`, `HOJE`, `SE`, `ÍNDICE`, `CORRESP`, validação de dados, formatação condicional
- Google Apps Script (JavaScript)

## Arquivos

| Arquivo | Descrição |
|---|---|
| `controle-day-off.xlsx` | Planilha com a base de dados e o painel |
| `aviso-day-off.gs` | Script que envia o aviso diário por e-mail |
| `painel.png` | Print do painel de consulta |

## Como usar

1. Abra `controle-day-off.xlsx` no Google Planilhas (Arquivo > Salvar como Google Planilhas).
2. Confirme que a aba de dados se chama `Planilha1`, com os dados a partir da linha 5 (nome na coluna B, nascimento na C e admissão na D).
3. Em **Extensões > Apps Script**, cole o conteúdo de `aviso-day-off.gs`.
4. Troque `seu-email@gmail.com` pelo seu e-mail.
5. Execute `enviarAvisoDayOff` para testar e autorize quando o Google pedir.
6. Execute `criarGatilho` uma vez para agendar o envio diário.

## Configurações do script

| Constante | O que faz |
|---|---|
| `NOME_ABA` | Nome da aba com os dados |
| `LINHA_INICIAL` | Primeira linha com dados |
| `EMAIL_DESTINO` | E-mail que recebe o aviso |
| `DIAS_ANTECEDENCIA` | Quantos dias antes do aniversário avisar |

## Limitações conhecidas

- Quem nasceu em 29 de fevereiro tem o aniversário contado em 1º de março nos anos não bissextos.
- O painel em Excel só mostra o aviso quando o arquivo é aberto. A notificação automática depende do script no Google Planilhas.
- A regra do day off (1 ano de empresa) está fixa no código e na fórmula.

## Próximos passos

- Enviar o aviso também pelo Teams ou WhatsApp.
- Migrar a base para um banco de dados SQL e criar uma API.

---

# Day Off Tracker (English version)

An Excel dashboard and a Google Apps Script that identify which employees are entitled to a day off on their birthday (after completing 1 year at the company) and send an email alert when a birthday is coming up.

> **All data in this repository is fictional.** The original version was created during an internship and was not published because it contained personal data (Brazilian data protection law, LGPD).

## Preview

!![Alert email](email-exemplo.png)

## The problem

Tracking birthday days off was done by hand. Each person's birth date and hire date had to be checked to find out who was entitled to the benefit and when.

## How it works

**Rule:** a person is entitled to the day off if, on the date of their next birthday, they will have completed 1 year at the company.

**Spreadsheet (Excel / Google Sheets)**
- **Planilha1 (data sheet):** database with name, birth date and hire date. It calculates time at the company, next birthday, days remaining, whether the person gets a day off, and an alert for the next 30 days.
- **Painel (dashboard):** lookup screen. Pick a promoter from the list to see their data and a warning message (for example, "TODAY is the birthday of ...: use day off!").

**Script (Google Apps Script)**
- Reads the data sheet and calculates who has a birthday today or in the coming days.
- Considers only people who will have 1 year at the company on the birthday date.
- Sends an alert email, and only sends one when there is someone to notify.
- Runs automatically every day, around 8 a.m., through a trigger.

## Technologies

- Excel and Google Sheets: `DATEDIF`, `TODAY`, `IF`, `INDEX`, `MATCH`, data validation, conditional formatting
- Google Apps Script (JavaScript)

## Files

| File | Description |
|---|---|
| `controle-day-off.xlsx` | Spreadsheet with the data sheet and the dashboard |
| `aviso-day-off.gs` | Script that sends the daily email alert |
| `painel.png` | Screenshot of the lookup dashboard |

## How to use

1. Open `controle-day-off.xlsx` in Google Sheets (File > Save as Google Sheets).
2. Make sure the data sheet is named `Planilha1`, with data starting at row 5 (name in column B, birth date in C, hire date in D).
3. Go to **Extensions > Apps Script** and paste the contents of `aviso-day-off.gs`.
4. Replace `seu-email@gmail.com` with your email address.
5. Run `enviarAvisoDayOff` to test it and grant permission when Google asks.
6. Run `criarGatilho` once to schedule the daily email.

## Script settings

| Constant | What it does |
|---|---|
| `NOME_ABA` | Name of the sheet with the data |
| `LINHA_INICIAL` | First row with data |
| `EMAIL_DESTINO` | Email address that receives the alert |
| `DIAS_ANTECEDENCIA` | How many days before the birthday to send the alert |

## Known limitations

- For people born on February 29, the birthday is counted as March 1 in non-leap years.
- The Excel dashboard only shows the alert when the file is opened. Automatic notification depends on the script running in Google Sheets.
- The day-off rule (1 year at the company) is fixed in the code and in the formulas.

## Next steps

- Also send the alert through Teams or WhatsApp.
- Move the data to a SQL database and build an API.
