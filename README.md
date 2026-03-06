# DESAFIO-QA-BEEDOO-2026

Repositório criado para o processo seletivo de Analista de Qualidade de Software Júnior da Beedoo.

---

## Sobre a aplicação

**URL:** https://creative-sherbet-a51eac.netlify.app/

A aplicação é um sistema simples de gerenciamento de cursos, voltado para cadastro, listagem e exclusão. Não há autenticação, o acesso é direto às funcionalidades.

Os três fluxos disponíveis são: cadastrar um curso via formulário, visualizar os cursos cadastrados em uma listagem, e excluir um curso existente.

---

## Como analisei

Comecei explorando a aplicação livremente, sem roteiro, só para entender o que estava disponível. Depois mapeei cada campo do formulário e pensei nos cenários que poderiam gerar problemas, tanto por uso incorreto quanto por tentativas maliciosas.

A partir disso, decidi focar em três frentes: validação dos campos, integridade dos dados (especialmente as datas) e segurança básica das entradas. São os pontos que se estiverem quebrados, comprometem o uso real da aplicação.

---

## Casos de teste

Foram criados 20 casos de teste no formato Gherkin (DADO / QUANDO / ENTÃO), cobrindo cenários positivos, negativos e alternativos.

Link para a planilha: https://docs.google.com/spreadsheets/d/1jlH9httxeXzL6NimSm8cClIfBihggrqYBT0WheFC26M/edit?usp=sharing
Link para o Google Drive (Evidências dos Testes): https://drive.google.com/drive/folders/1JyA9CVBAA5iauZfLMg_SOc_vGp9Dt5c6?usp=drive_link

---

## Bugs encontrados

| ID | Severidade | Título |
|---|---|---|
| BUG-001 | Crítica | Sistema aceita cadastro com data de início posterior a data de fim 
| BUG-002 | Alta | Campo de vagas aceita valores negativos e zero 
| BUG-003 | Crítica | Formulário permite cadastro com todos os campos em branco 
| BUG-004 | Alta | Campo 'Nome do Curso' não é obrigatório 
| BUG-005 | Média | URL de imagem não é validada 
| BUG-006 | Baixa | Listagem vazia não exibe mensagem informativa 
| BUG-007 | Crítica | Campo 'Nome' aceita e renderiza caracteres HTML, possível XSS 
| BUG-008 | Média | Layout da listagem quebra com múltiplos cursos cadastrados 
| BUG-009 | Crítica | Exclusão não é efetivada, mas o sistema exibe mensagem de sucesso 

O relatório completo com passos para reproduzir, resultado atual e esperado está na aba "Relatório de Bugs" da planilha acima.

---

## Análise e tomada de decisão

**Priorização dos bugs**

Os bugs críticos (BUG-003, BUG-007 e BUG-009) seriam tratados primeiro. A ausência de validação compromete a integridade dos dados, o XSS é uma vulnerabilidade de segurança real, e o BUG-009 é agravado pelo fato de o sistema confirmar uma ação que não aconteceu. Na sequência, BUG-001 e BUG-004, que também afetam diretamente os dados. Os demais seguiriam por ordem de impacto.

**Investigação de defeitos difíceis de reproduzir**

Primeiro coletaria o máximo de contexto: browser, sistema, dados usados e passos exatos. Depois tentaria isolar variáveis, testar em outros browsers, dispositivos e redes. Verificaria o console e as requisições de rede pelo DevTools. Se ainda não reproduzisse, documentaria mesmo assim e classificaria como intermitente.

**Vulnerabilidades identificadas**

O campo de nome aceita HTML sem sanitização, o que abre brecha para XSS. Nenhum campo do formulário é validado, o que facilita entradas maliciosas. Se houver back-end com banco de dados, a ausência de sanitização também abre risco para SQL Injection. O botão salvar não é desabilitado depois do clique, permitindo envio duplicado de requisições.

**Bug crítico véspera de release**

Comunicaria o time imediatamente com todos os detalhes. Avaliaria em conjunto o impacto real e proporia três caminhos: corrigir antes da release, adiar, ou liberar com o bug documentado e plano de hotfix.

---

## Uso de IA

Usei IA como apoio na estruturação do Google Sheets e nos possíveis casos de bugs relacionados ao contexto da aplicação de cursos. As decisões de análise, a execução dos testes, a identificação dos bugs e a priorização de cada problema foram feitas por mim, com base no que observei diretamente no sistema.

---

*Ruhan Freitas | Desafio Beedoo 2026*
