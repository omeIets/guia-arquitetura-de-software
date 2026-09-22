A escolha de qualquer estilo arquitetural implica aceitar compromissos: atributos de qualidade que são favorecidos em detrimento de outros [@richards2020fundamentals]. Na arquitetura em camadas, esses compromissos decorrem diretamente da regra de separação de responsabilidades e do fluxo unidirecional de dependências, princípios formalizados no padrão *Layers* descrito por Buschmann et al. [-@buschmann1996pattern, cap. 2].

### Atributos favorecidos

A **manutenibilidade** é o benefício mais evidente. Quando a interface entre duas camadas adjacentes é preservada, alterações internas em uma delas — como a troca de um framework de persistência — não se propagam para as demais [@bass2003practice, cap. 5]. Essa propriedade viabiliza, por exemplo, a migração de um banco relacional para um não relacional sem que a camada de domínio precise ser modificada. De forma análoga, a **portabilidade** é favorecida: substituir toda a camada de apresentação (de uma interface Web para uma aplicação mobile) torna-se viável sem reescrever a lógica de negócio, desde que os contratos entre camadas permaneçam estáveis [@sommerville2011engenharia, cap. 6].

A **testabilidade** também é fortalecida pelo isolamento. Cada camada pode ser verificada de forma independente, utilizando dublês de teste (*stubs* ou *mocks*) para simular o comportamento das camadas adjacentes [@bass2003practice, cap. 5]. Isso reduz a complexidade dos cenários de teste e permite que defeitos sejam localizados com mais precisão. Além disso, o **reuso** de camadas inferiores é facilitado: uma mesma camada de domínio pode ser compartilhada por múltiplas interfaces ou consumida por serviços distintos, eliminando duplicação de lógica [@sommerville2011engenharia, cap. 6]. Fowler [-@fowler2015presentation] reforça que essa separação entre apresentação, domínio e dados é o alicerce para qualquer estratégia de reuso consistente.

### Atributos sacrificados

O **desempenho** é o custo mais frequentemente associado a esse estilo. Cada requisição precisa atravessar todas as camadas intermediárias — mesmo quando a operação é trivial —, acumulando latência de serialização, transformação de dados e chamadas entre fronteiras [@bass2003practice, cap. 5]. Em cenários de alta vazão, esse *overhead* pode tornar-se significativo, sobretudo se comparado a uma arquitetura monolítica sem separação lógica, na qual a comunicação entre componentes ocorre por chamadas diretas em memória.

A **simplicidade** é igualmente comprometida. A adição de camadas introduz mais indireção: o desenvolvedor precisa navegar por múltiplos módulos para rastrear o fluxo de uma operação de ponta a ponta. Segundo Sommerville [-@sommerville2011engenharia, cap. 6], essa complexidade estrutural exige que a equipe invista em convenções claras de organização, sob pena de tornar o sistema mais difícil de compreender do que a versão não estratificada.

Por fim, existe o risco de **acoplamento vertical** entre camadas adjacentes. Embora a arquitetura proíba dependências ascendentes, cada camada depende diretamente da interface da camada imediatamente abaixo. Mudanças estruturais nessa interface — como a alteração de um contrato de serviço — podem exigir ajustes em todas as camadas superiores, configurando as chamadas *mudanças em cascata* [@bass2003practice, cap. 5].

| Atributo | Efeito | Justificativa |
|---|---|---|
| Manutenibilidade | Favorecida | Mudança interna em uma camada não propaga, desde que a interface se mantenha |
| Portabilidade | Favorecida | Camadas superiores podem ser substituídas sem afetar as inferiores |
| Testabilidade | Favorecida | Camadas isoláveis permitem testes com dublês independentes |
| Reuso | Favorecido | Camadas inferiores podem servir a múltiplas interfaces |
| Desempenho | Comprometido | Cada requisição atravessa todas as camadas, somando latência |
| Simplicidade | Comprometida | Mais indireção do que uma arquitetura monolítica sem camadas |
| Acoplamento vertical | Risco | Mudanças na interface de uma camada inferior podem propagar-se para cima |
