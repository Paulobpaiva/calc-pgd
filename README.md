<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Horas</title>
    <style>
        body {
            display: flex;
            background-color: black;
            color: white;
        }
        .container {
            flex: 1;
            padding: 20px;
        }
        #calculator {
            border: 1px solid #ccc;
            padding: 10px;
            width: 200px;
            background-color: grey;
            color: black;
        }
        .footer {
            font-style: italic;
            font-size: small;
            text-align: right;
            color: grey;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2 style="color: grey;">Confira os feriados e pontos facultativos de 2024</h2>
        <ul>
            <li>1º de janeiro, Confraternização Universal (feriado nacional)</li>
            <li>12 de fevereiro, Carnaval (ponto facultativo)</li>
            <li>13 de fevereiro, Carnaval (ponto facultativo)</li>
            <li>14 de fevereiro, Quarta-Feira de Cinzas (ponto facultativo até as 14h)</li>
            <li>29 de março, Paixão de Cristo (feriado nacional)</li>
            <li>21 de abril, Tiradentes (feriado nacional)</li>
            <li>1º de maio, Dia Mundial do Trabalho (feriado nacional)</li>
            <li>30 de maio, Corpus Christi (ponto facultativo)</li>
            <li>31 de maio (ponto facultativo)</li>
            <li>7 de setembro, Independência do Brasil (feriado nacional)</li>
            <li>12 de outubro, Nossa Senhora Aparecida (feriado nacional)</li>
            <li>28 de outubro, Dia do Servidor Público federal (ponto facultativo)</li>
            <li>2 de novembro, Finados (feriado nacional)</li>
            <li>15 de novembro, Proclamação da República (feriado nacional)</li>
            <li>20 de novembro, Dia Nacional de Zumbi e da Consciência Negra (feriado nacional)</li>
            <li>24 de dezembro, Véspera do Natal (ponto facultativo após as 14h)</li>
            <li>25 de dezembro, Natal (feriado nacional)</li>
            <li>31 de dezembro, Véspera do Ano Novo (ponto facultativo após as 14h)</li>
            <!-- Outros feriados e pontos facultativos -->
        </ul>
        <p style="color: grey;">Fonte: Disponível em: <a href="https://www.gov.br/inss/pt-br/assuntos/confira-os-feriados-e-pontos-facultativo-do-proximo-ano-1" target="_blank">https://www.gov.br/inss/pt-br/assuntos/confira-os-feriados-e-pontos-facultativo-do-proximo-ano-1</a></p>
    </div>
    <div class="container">
        <h2 style="color: grey;">Calculadora de Horas</h2>
        <div id="calculator">
            <label for="startDate">Data de Início:</label>
            <input type="date" id="startDate"><br><br>
            <label for="endDate">Data de Fim:</label>
            <input type="date" id="endDate"><br><br>
            <label for="subtractedHours">Horas Subtraídas:</label>
            <input type="number" id="subtractedHours" value="0"><br><br>
            <button onclick="calculateHours()">Calcular</button><br><br>
            <div id="result"></div>
        </div>
        <div class="footer">
            <p>Paulo B. Paiva Melo</p>
        </div>
    </div>

    <script>
        function calculateHours() {
            var startDate = new Date(document.getElementById('startDate').value);
            var endDate = new Date(document.getElementById('endDate').value);
            var subtractedHours = parseInt(document.getElementById('subtractedHours').value);

            var millisecondsPerDay = 1000 * 60 * 60 * 24;
            var totalDays = 0;
            var currentDate = new Date(startDate);

            // Loop through each day between start and end dates
            while (currentDate <= endDate) {
                var dayOfWeek = currentDate.getDay();
                // Check if it's a weekday (Monday to Friday)
                if (dayOfWeek >= 1 && dayOfWeek <= 5) {
                    // Check if it's not a holiday or facultative point
                    if (!isHoliday(currentDate)) {
                        totalDays++;
                    }
                }
                currentDate.setDate(currentDate.getDate() + 1);
            }

            var totalHours = totalDays * 8 - subtractedHours;

            document.getElementById('result').innerHTML = "Total de horas trabalhadas: " + totalHours.toFixed(2) + " horas";
        }

        function isHoliday(date) {
            var holidays = [
                new Date(2024, 0, 1), // 1º de janeiro
                new Date(2024, 1, 12), // 12 de fevereiro
                new Date(2024, 1, 13), // 13 de fevereiro
                new Date(2024, 1, 14), // 14 de fevereiro
                new Date(2024, 2, 29), // 29 de março
                new Date(2024, 3, 21), // 21 de abril
                new Date(2024, 4, 1), // 1º de maio
                new Date(2024, 4, 30), // 30 de maio
                new Date(2024, 5, 31), // 31 de maio
                new Date(2024, 8, 7), // 7 de setembro
                new Date(2024, 9, 12), // 12 de outubro
                new Date(2024, 9, 28), // 28 de outubro
                new Date(2024, 10, 2), // 2 de novembro
                new Date(2024, 10, 15), // 15 de novembro
                new Date(2024, 10, 20), // 20 de novembro
                new Date(2024, 11, 24), // 24 de dezembro
                new Date(2024, 11, 25), // 25 de dezembro
                new Date(2024, 11, 31) // 31 de dezembro
            ];

            for (var i = 0; i < holidays.length; i++) {
                if (date.getTime() === holidays[i].getTime()) {
                    return true;
                }
            }

            return false;
        }
    </script>
</body>
</html>
