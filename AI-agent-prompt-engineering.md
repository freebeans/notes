# AI Agents Prompt Engineering
Resumo à partir de: [Building AI Agents: Prompt Engineering for Beginners [Part 3]
](https://www.youtube.com/watch?v=77Z07QnLlB8)

## 3 Layers of Prompting

### System layer
|Etapa|Descrição|
|-|-|
|**Papel**|Quem é você e qual é seu papel|
|**Instruções**|Lista de tarefas e sub-tarefas. Pode ter um prefácio, ex.: "use as instruções abaixo para fazer **xxx**"|
|**Regras**|Regrinhas como `não use markdown`, `não invente respostas`, `peça mais informações se precisar`, `sempre responda em português`|
|**Exemplos**| Exemplos de mensagens consistentes para resultados esperados, como o formato de uma mensagem de sucesso, de erro, etc. Ex.: `Esta é uma pergunta mais complexa, vou repassar o atendimento para um especialista.` |
|**Contexto adicional**| Expressões dinâmicas que informem dia da semana, data, hora, nome do cliente, nome da loja/escritório, telefone/contato, etc.|
|**Reduzindo alucinações**| Permitir que o agente diga que não sabe pode reduzir drasticamente ocorrências de informação falsa. Pedir para que copie exatamente trechos de texto relevantes para responder uma pergunta pode melhorar respostas baseadas em RAG. Pedir para que o modelo explique sua linha de raciocínio pode revelar problemas lógicos e pré-suposições erradas (bom para debugar). |

### Input layer
Se o agente não estiver sendo usado por um chat e sim por uma API, formular o input com valores dinâmicos, contexto suficiente e palavras-chave do *System prompt*.

### Action layer
**Nome da ferramenta:** evitar espaços (preferir *underscore*), evitar termos comuns. Você não quer que o nome da ferramenta seja confundido com alguma informação presente no treinamento do modelo. Usar o nome exato ao referenciar a ferramenta no *System prompt*.

**Campos dinâmicos:** usar o método `$fromAI()` do n8n com um nome relevante (referenciado na descrição) e possivelmente a descrição de formato.

**Descrição:** deve instruir o que a ferramenta faz. É melhor deixar detalhes mais específicos aqui, ao invés de especificar tudo no *System prompt*. Isso facilita reutilização da ferramenta e permite alterações futuras nas ferramentas sem precisar mexer no prompt (ex.: trocar um app de calendário por outro).

Exemplo: "Use esta ferramenta **nome_da_ferramenta** para listar agendamentos no calendário e determinar quando há horários vagos."

A descrição pode conter ainda instruções de como extrair a informação desejada à partir do que a ferramenta retorna. Exemplo: "Quando souber os horários preenchidos, calcule os horários vagos garantindo que não haja sobreposição de horários com outros agendamentos."
