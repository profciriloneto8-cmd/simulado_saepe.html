# simulado_saepe.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulado SAEPE/SAEB Interativo - Matemática</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
            padding: 30px;
        }
        
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
        }
        
        .instructions {
            background-color: #e8f4fc;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
            border-left: 4px solid #3498db;
        }
        
        .question {
            margin-bottom: 25px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        
        .question-number {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 1.1em;
        }
        
        .options {
            margin-top: 10px;
        }
        
        .option {
            margin: 8px 0;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .option:hover {
            background-color: #eef7ff;
        }
        
        .option.selected {
            background-color: #d4edda;
            border: 1px solid #c3e6cb;
        }
        
        .option.correct {
            background-color: #d4edda;
            border: 1px solid #c3e6cb;
        }
        
        .option.incorrect {
            background-color: #f8d7da;
            border: 1px solid #f5c6cb;
        }
        
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px 5px;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #2980b9;
        }
        
        button:disabled {
            background-color: #bdc3c7;
            cursor: not-allowed;
        }
        
        .result {
            margin-top: 30px;
            padding: 20px;
            border-radius: 5px;
            text-align: center;
            display: none;
        }
        
        .result.good {
            background-color: #d4edda;
            border: 1px solid #c3e6cb;
            color: #155724;
        }
        
        .result.average {
            background-color: #fff3cd;
            border: 1px solid #ffeaa7;
            color: #856404;
        }
        
        .result.poor {
            background-color: #f8d7da;
            border: 1px solid #f5c6cb;
            color: #721c24;
        }
        
        .progress-bar {
            height: 10px;
            background-color: #ecf0f1;
            border-radius: 5px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: #3498db;
            width: 0%;
            transition: width 0.5s;
        }
        
        .feedback {
            margin-top: 15px;
            padding: 10px;
            border-radius: 5px;
            display: none;
        }
        
        .feedback.correct {
            background-color: #d4edda;
            border: 1px solid #c3e6cb;
            color: #155724;
        }
        
        .feedback.incorrect {
            background-color: #f8d7da;
            border: 1px solid #f5c6cb;
            color: #721c24;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        .question-counter {
            text-align: center;
            margin: 15px 0;
            font-weight: bold;
            color: #7f8c8d;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Simulado SAEPE/SAEB - Matemática - Ensino Médio</h1>
        
        <div class="instructions">
            <p><strong>Instruções:</strong></p>
            <ol>
                <li>Leia cada questão com atenção.</li>
                <li>Selecione a alternativa que você considera correta.</li>
                <li>Você pode navegar entre as questões usando os botões "Anterior" e "Próxima".</li>
                <li>Após responder todas as questões, clique em "Finalizar Simulado" para ver seu resultado.</li>
            </ol>
        </div>
        
        <div class="question-counter">Questão <span id="current-question">1</span> de 10</div>
        
        <div class="progress-bar">
            <div class="progress" id="progress-bar"></div>
        </div>
        
        <div id="questions-container">
            <!-- As questões serão inseridas aqui via JavaScript -->
        </div>
        
        <div class="navigation">
            <button id="prev-btn" disabled>Anterior</button>
            <button id="next-btn">Próxima</button>
        </div>
        
        <div style="text-align: center; margin-top: 20px;">
            <button id="submit-btn">Finalizar Simulado</button>
        </div>
        
        <div id="result" class="result"></div>
    </div>

    <script>
        // Dados das questões
        const questions = [
            {
                number: 1,
                descriptor: "D1 – Identificar padrões numéricos ou princípios de contagem",
                question: "Observe a sequência numérica: 2, 5, 11, 23, 47, ... Mantendo o mesmo padrão, o próximo termo dessa sequência será:",
                options: ["71", "83", "95", "101", "119"],
                correctAnswer: 2, // Índice da opção correta (0-based)
                explanation: "Padrão: multiplicar por 2 e somar 1. 2×2+1=5; 5×2+1=11; 11×2+1=23; 23×2+1=47; 47×2+1=95."
            },
            {
                number: 2,
                descriptor: "D2 – Identificar propriedades de figuras geométricas planas",
                question: "Um terreno tem a forma de um triângulo retângulo. Se os catetos medem 6 m e 8 m, a medida da hipotenusa, em metros, é:",
                options: ["10", "12", "14", "16", "18"],
                correctAnswer: 0,
                explanation: "Teorema de Pitágoras: h² = 6² + 8² = 36 + 64 = 100 → h = 10 m."
            },
            {
                number: 3,
                descriptor: "D3 – Resolver problema envolvendo relações métricas no triângulo retângulo",
                question: "Uma escada de 5 metros de comprimento está apoiada em uma parede. Se a base da escada está afastada 3 metros da parede, a que altura do chão, em metros, o topo da escada toca a parede?",
                options: ["3,5", "4", "4,5", "5", "5,5"],
                correctAnswer: 1,
                explanation: "Teorema de Pitágoras: altura² + 3² = 5² → altura² + 9 = 25 → altura² = 16 → altura = 4 m."
            },
            {
                number: 4,
                descriptor: "D4 – Resolver problema envolvendo equação do 1º grau",
                question: "Carlos comprou uma camiseta e um boné por R$ 65,00. Sabendo que a camiseta custou R$ 15,00 a mais que o boné, qual era o preço do boné?",
                options: ["R$ 20,00", "R$ 25,00", "R$ 30,00", "R$ 35,00", "R$ 40,00"],
                correctAnswer: 1,
                explanation: "Equação: x + (x + 15) = 65 → 2x + 15 = 65 → 2x = 50 → x = 25. Boné = R$ 25,00."
            },
            {
                number: 5,
                descriptor: "D5 – Resolver problema envolvendo sistemas de equações do 1º grau",
                question: "Em uma lanchonete, 2 sanduíches e 3 sucos custam R$ 32,00. Já 3 sanduíches e 2 sucos custam R$ 33,00. Qual é o preço de um sanduíche?",
                options: ["R$ 6,00", "R$ 7,00", "R$ 8,00", "R$ 9,00", "R$ 10,00"],
                correctAnswer: 1,
                explanation: "Sistema: 2s + 3j = 32; 3s + 2j = 33. Resolvendo: s = R$ 7,00."
            },
            {
                number: 6,
                descriptor: "D6 – Resolver problema envolvendo porcentagem",
                question: "Em uma turma de 40 alunos, 55% são meninas. Quantos meninos há nessa turma?",
                options: ["18", "20", "22", "24", "25"],
                correctAnswer: 0,
                explanation: "Meninas: 55% de 40 = 0,55×40 = 22. Meninos = 40 – 22 = 18."
            },
            {
                number: 7,
                descriptor: "D7 – Resolver problema envolvendo grandezas diretamente ou inversamente proporcionais",
                question: "Se 6 operários constroem um muro em 10 dias, em quantos dias 8 operários, com a mesma capacidade, construiriam o mesmo muro?",
                options: ["7,0", "7,5", "8,0", "8,5", "9,0"],
                correctAnswer: 1,
                explanation: "Grandezas inversamente proporcionais: 6 × 10 = 8 × x → 60 = 8x → x = 7,5 dias."
            },
            {
                number: 8,
                descriptor: "D8 – Resolver problema envolvendo área de figuras planas",
                question: "Uma praça circular tem raio de 20 m. Qual é a área, em m², dessa praça? (Use π = 3,14)",
                options: ["628", "1256", "1884", "2512", "3140"],
                correctAnswer: 1,
                explanation: "Área do círculo: A = πr² = 3,14 × 20² = 3,14 × 400 = 1256 m²."
            },
            {
                number: 9,
                descriptor: "D9 – Resolver problema envolvendo volume de sólidos geométricos",
                question: "Uma caixa-d'água tem a forma de um paralelepípedo retângulo com dimensões 2 m × 3 m × 4 m. Qual é o volume dessa caixa-d'água, em litros? (Lembre-se: 1 m³ = 1000 L)",
                options: ["24.000 L", "20.000 L", "18.000 L", "15.000 L", "12.000 L"],
                correctAnswer: 0,
                explanation: "Volume: V = 2 × 3 × 4 = 24 m³. Em litros: 24 × 1000 = 24.000 L."
            },
            {
                number: 10,
                descriptor: "D10 – Resolver problema envolvendo média aritmética",
                question: "As notas de um aluno em cinco provas de Matemática foram: 7,0; 8,0; 6,5; 9,0 e 7,5. Qual foi a média aritmética dessas notas?",
                options: ["7,4", "7,6", "7,8", "8,0", "8,2"],
                correctAnswer: 1,
                explanation: "Média: (7,0 + 8,0 + 6,5 + 9,0 + 7,5) / 5 = 38 / 5 = 7,6."
            }
        ];

        // Variáveis de estado
        let currentQuestionIndex = 0;
        let userAnswers = new Array(questions.length).fill(null);
        let quizSubmitted = false;

        // Elementos do DOM
        const questionsContainer = document.getElementById('questions-container');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const submitBtn = document.getElementById('submit-btn');
        const resultDiv = document.getElementById('result');
        const currentQuestionSpan = document.getElementById('current-question');
        const progressBar = document.getElementById('progress-bar');

        // Inicializar o simulado
        function initializeQuiz() {
            renderQuestion(currentQuestionIndex);
            updateNavigationButtons();
            updateProgressBar();
        }

        // Renderizar a questão atual
        function renderQuestion(index) {
            const question = questions[index];
            currentQuestionSpan.textContent = index + 1;
            
            let optionsHTML = '';
            question.options.forEach((option, i) => {
                const isSelected = userAnswers[index] === i;
                const isCorrect = quizSubmitted && i === question.correctAnswer;
                const isIncorrect = quizSubmitted && userAnswers[index] === i && i !== question.correctAnswer;
                
                let optionClass = 'option';
                if (isSelected) optionClass += ' selected';
                if (isCorrect) optionClass += ' correct';
                if (isIncorrect) optionClass += ' incorrect';
                
                optionsHTML += `
                    <div class="${optionClass}" data-index="${i}">
                        ${String.fromCharCode(65 + i)}) ${option}
                    </div>
                `;
            });
            
            questionsContainer.innerHTML = `
                <div class="question">
                    <div class="question-number">Questão ${question.number} - ${question.descriptor}</div>
                    <div>${question.question}</div>
                    <div class="options">${optionsHTML}</div>
                    ${quizSubmitted ? `
                        <div class="feedback ${userAnswers[index] === question.correctAnswer ? 'correct' : 'incorrect'}">
                            <strong>${userAnswers[index] === question.correctAnswer ? 'Resposta Correta!' : 'Resposta Incorreta'}</strong><br>
                            ${question.explanation}
                        </div>
                    ` : ''}
                </div>
            `;
            
            // Adicionar event listeners para as opções (apenas se o simulado não foi submetido)
            if (!quizSubmitted) {
                document.querySelectorAll('.option').forEach(option => {
                    option.addEventListener('click', () => {
                        const selectedIndex = parseInt(option.getAttribute('data-index'));
                        userAnswers[index] = selectedIndex;
                        renderQuestion(index);
                        updateProgressBar();
                    });
                });
            }
        }

        // Atualizar botões de navegação
        function updateNavigationButtons() {
            prevBtn.disabled = currentQuestionIndex === 0;
            nextBtn.disabled = currentQuestionIndex === questions.length - 1;
            
            if (currentQuestionIndex === questions.length - 1) {
                submitBtn.style.display = 'inline-block';
            } else {
                submitBtn.style.display = 'none';
            }
        }

        // Atualizar barra de progresso
        function updateProgressBar() {
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const progress = (answeredCount / questions.length) * 100;
            progressBar.style.width = ${progress}%;
        }

        // Navegar para a próxima questão
        function nextQuestion() {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                renderQuestion(currentQuestionIndex);
                updateNavigationButtons();
            }
        }

        // Navegar para a questão anterior
        function prevQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                renderQuestion(currentQuestionIndex);
                updateNavigationButtons();
            }
        }

        // Finalizar o simulado e mostrar resultados
        function submitQuiz() {
            quizSubmitted = true;
            const answeredCount = userAnswers.filter(answer => answer !== null).length;
            const correctCount = userAnswers.reduce((count, answer, index) => {
                return count + (answer === questions[index].correctAnswer ? 1 : 0);
            }, 0);
            
            const score = (correctCount / questions.length) * 100;
            
            let resultClass = 'result ';
            let message = '';
            
            if (score >= 80) {
                resultClass += 'good';
                message = Parabéns! Você acertou ${correctCount} de ${questions.length} questões (${score.toFixed(1)}%). Excelente desempenho!;
            } else if (score >= 60) {
                resultClass += 'average';
                message = Bom trabalho! Você acertou ${correctCount} de ${questions.length} questões (${score.toFixed(1)}%). Continue estudando para melhorar ainda mais!;
            } else {
                resultClass += 'poor';
                message = Você acertou ${correctCount} de ${questions.length} questões (${score.toFixed(1)}%). Reveja os conteúdos e tente novamente!;
            }
            
            resultDiv.className = resultClass;
            resultDiv.innerHTML = `
                <h2>Resultado do Simulado</h2>
                <p>${message}</p>
                <p><strong>Descritores que você precisa revisar:</strong></p>
                <ul>
                    ${questions.map((q, i) => 
                        userAnswers[i] !== q.correctAnswer ? <li>${q.descriptor}</li> : ''
                    ).join('')}
                </ul>
                <button onclick="location.reload()">Fazer Novamente</button>
            `;
            resultDiv.style.display = 'block';
            
            // Rolar para o resultado
            resultDiv.scrollIntoView({ behavior: 'smooth' });
            
            // Re-renderizar a questão atual para mostrar o feedback
            renderQuestion(currentQuestionIndex);
            
            // Desabilitar botões
            prevBtn.disabled = true;
            nextBtn.disabled = true;
            submitBtn.disabled = true;
        }

        // Event listeners
        prevBtn.addEventListener('click', prevQuestion);
        nextBtn.addEventListener('click', nextQuestion);
        submitBtn.addEventListener('click', submitQuiz);

        // Inicializar o simulado
        initializeQuiz();
    </script>
</body>
</html>
