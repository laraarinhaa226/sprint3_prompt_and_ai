# Relatório de Comparação entre Modelos — Sprint 03

## Modelos avaliados

Testamos dois modelos: o `gpt-4o-mini` e o `gpt-5-nano`. Não conseguimos testar o `gpt-4o` porque a conta da OpenAI utilizada não tinha acesso a esse modelo.

## Configurações utilizadas

Nas duas rodadas de teste, utilizamos o mesmo agente, com as mesmas instruções, as mesmas ferramentas e os mesmos guardrails de segurança. A única coisa que mudou foi o modelo do agente principal. Os agentes responsáveis pelos guardrails ficaram sempre com o `gpt-4o-mini`, pra garantir que qualquer diferença encontrada viesse do modelo principal e não dos guardrails. Não mexemos em parâmetros como temperatura, já que utilizamos os valores padrão do framework.

## Resultados obtidos

Rodamos as mesmas perguntas nos dois modelos: as 5 perguntas de teste da Sprint 1 e 2, o teste de memória com 3 mensagens seguidas, o teste de tentativa de burlar o chatbot (prompt injection), o teste de perguntar uma especificação técnica inventada, e o teste de pedir conselho jurídico e financeiro.

Com o `gpt-4o-mini`, todas as respostas saíram como esperado. As perguntas sobre consumo e tempo de recarga pediram o número da sessão antes de responder, o que é um comportamento novo em relação à Sprint 2, mas correto. A memória funcionou nos 3 turnos. As tentativas de prompt injection e os pedidos de conselho jurídico/financeiro foram bloqueados corretamente. E o chatbot não inventou nenhuma especificação técnica quando perguntamos sobre um modelo de carregador que não existe.

Com o `gpt-5-nano`, o resultado foi parecido, mas com uma diferença importante: no teste de memória, a primeira mensagem foi bloqueada por engano pelo guardrail de saída, achando que a resposta era perigosa quando não era. Mesmo assim, o chatbot continuou lembrando da informação nas mensagens seguintes, então a memória em si funcionou, só a resposta da primeira mensagem foi perdida. Os outros testes funcionaram bem, do mesmo jeito que no `gpt-4o-mini`.

## Diferenças entre os modelos

O `gpt-5-nano` escreve respostas bem mais longas e detalhadas. Ele explica mais opções, entra em mais detalhes técnicos e já se antecipa oferecendo ajuda extra, como abrir um chamado de suporte antes mesmo de ser pedido. O `gpt-4o-mini` é mais direto e mais curto nas respostas.

Também observamos que, por ser mais detalhado, o `gpt-5-nano` às vezes usa termos técnicos que fizeram o guardrail de segurança bloquear a resposta por engano. Isso não aconteceu com o `gpt-4o-mini` durante os testes.

## Vantagens e limitações de cada um

O `gpt-4o-mini` tem como vantagem ser mais previsível: em todos os nossos testes ele respondeu do jeito esperado, sem nenhum bloqueio incorreto. Como limitação, ele é menos proativo e às vezes dá respostas mais genéricas.

O `gpt-5-nano` tem como vantagem dar respostas mais completas e detalhadas, cobrindo mais situações que o usuário pode ter. Como limitação, ele gastou mais texto em cada resposta, e num dos nossos testes acabou sendo bloqueado sem necessidade, o que pode atrapalhar a experiência de quem está usando o chatbot.

## Modelo escolhido para a versão final

Escolhemos o `gpt-4o-mini`.

## Justificativa da escolha

Num chatbot de atendimento ao cliente, é mais importante o chatbot responder sempre do mesmo jeito confiável do que dar respostas mais longas e detalhadas. Como o `gpt-5-nano` acabou tendo uma resposta legítima bloqueada por engano durante os testes, e o `gpt-4o-mini` não teve nenhum problema desse tipo, decidimos seguir com o `gpt-4o-mini` na versão final do projeto.

