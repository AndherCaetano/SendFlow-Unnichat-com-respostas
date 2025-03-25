<html lang="pt-BR">
<head> 
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teste Unnichat - Respostas</title>
    <style>
        /* [Manter todos os estilos CSS anteriores] */
        /* ... (todo o CSS anterior permanece exatamente igual) ... */
    </style>
    <!-- Biblioteca para gerar PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
</head>
<body>
    <!-- [Manter todo o conteúdo HTML anterior] -->
    <!-- ... (todo o HTML anterior permanece exatamente igual) ... -->

    <script>
        async function sendByEmail() {
            const element = document.getElementById('form-content');
            const buttons = document.querySelector('.action-buttons');
            buttons.style.display = 'none'; // Esconde os botões temporariamente
            
            try {
                // Configurações do PDF melhoradas
                const opt = {
                    margin: [10, 10, 10, 10],
                    filename: 'Respostas_Atividades_Unnichat.pdf',
                    image: { type: 'jpeg', quality: 1 },
                    html2canvas: { 
                        scale: 2,
                        logging: false,
                        useCORS: true,
                        allowTaint: true,
                        scrollX: 0,
                        scrollY: 0,
                        windowWidth: element.scrollWidth,
                        windowHeight: element.scrollHeight
                    },
                    jsPDF: { 
                        unit: 'mm', 
                        format: 'a4', 
                        orientation: 'portrait',
                        compress: true
                    },
                    pagebreak: { mode: 'avoid-all' }
                };
                
                // Gera o PDF com configurações aprimoradas
                const pdf = await html2pdf().set(opt).from(element).toPdf().get('pdf');
                
                // Cria o blob do PDF
                const pdfBlob = pdf.output('blob');
                const pdfUrl = URL.createObjectURL(pdfBlob);
                
                const subject = "Respostas Atividades Unnichat";
                const emailTo = "shi@sendflow.com.br";
                const emailCC = "luiz@sendflow.pro";
                const body = "Segue em anexo as respostas completas do questionário Unnichat, conforme solicitado.";
                
                // Cria link temporário para download do PDF
                const tempLink = document.createElement('a');
                tempLink.href = pdfUrl;
                tempLink.download = opt.filename;
                document.body.appendChild(tempLink);
                tempLink.click();
                document.body.removeChild(tempLink);
                
                // Abre o cliente de e-mail com o PDF anexado
                window.location.href = `mailto:${emailTo}?cc=${emailCC}&subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
                
            } catch (error) {
                console.error("Erro ao gerar PDF:", error);
                alert("Ocorreu um erro ao gerar o PDF. Por favor, tente novamente.");
            } finally {
                buttons.style.display = ''; // Mostra os botões novamente
            }
        }

        function sendByWhatsApp() {
            const phoneNumber = "5511996504486";
            const message = "Boa tarde, Seguem respostas realizadas para os exercícios\n\n";
            
            // Coleta todas as perguntas e respostas
            let fullText = message;
            
            // Parte 1
            fullText += "═══════════════\n*PARTE 1*\n═══════════════\n";
            const part1Questions = document.querySelectorAll('.part:nth-of-type(1) .question');
            part1Questions.forEach((question, index) => {
                const label = question.querySelector('label').textContent.trim();
                const answer = question.querySelector('.answer').textContent.trim();
                fullText += `\n*${index + 1}. ${label}*\n${answer}\n`;
            });
            
            // Parte 2
            fullText += "\n═══════════════\n*PARTE 2*\n═══════════════\n";
            const part2Questions = document.querySelectorAll('.part:nth-of-type(2) .question');
            part2Questions.forEach((question, index) => {
                const label = question.querySelector('label').textContent.trim();
                const answer = question.querySelector('.answer').textContent.trim();
                fullText += `\n*${index + 1}. ${label}*\n${answer}\n`;
            });
            
            // Parte 3
            fullText += "\n═══════════════\n*PARTE 3*\n═══════════════\n";
            const part3Questions = document.querySelectorAll('.part:nth-of-type(3) .question');
            part3Questions.forEach((question, index) => {
                const label = question.querySelector('label').textContent.trim();
                const answer = question.querySelector('.answer').textContent.trim();
                fullText += `\n*${index + 1}. ${label}*\n${answer}\n`;
            });
            
            // Codifica a mensagem para URL
            const encodedMessage = encodeURIComponent(fullText);
            
            // Abre o WhatsApp
            window.open(`https://wa.me/${phoneNumber}?text=${encodedMessage}`, '_blank');
        }
    </script>
</body>
</html>
