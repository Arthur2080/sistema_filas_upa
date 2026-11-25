# Mudança de escopo: de hospitais para UPAs

**Data:** 25/11/2026

O projeto passou a tratar só das **UPAs (Unidades de Pronto Atendimento)**, e não mais de prontos-socorros
de hospitais maiores. Os textos que falavam em "hospital", "pronto-socorro" ou "Pronto-Atendimento" foram
trocados por "UPA". Os cálculos, as regras de negócio e o funcionamento do sistema não mudaram.

## Mudanças feitas

### Código e README

| Arquivo | Antes | Depois |
|---|---|---|
| `README.md` (título) | Pronto-Atendimento — Simulador de espera | UPA — Simulador de espera |
| `README.md` (descrição) | pacientes de um pronto-socorro | pacientes de uma UPA (Unidade de Pronto Atendimento) |
| `frontend/index.html` (título da aba) | Pronto-Atendimento · Simulador de espera | UPA · Simulador de espera |
| `frontend/index.html` (cabeçalho) | Pronto-Atendimento | UPA 24h |
| `frontend/js/app.js` (comentário) | Simulador de espera do pronto-socorro | Simulador de espera da UPA |
| `backend/ProtocoloManchester.java` (comentário) | triagem do pronto-socorro | triagem da UPA |

### Slide (`docs/SlideProjeto.html`)

| Slide | Antes | Depois |
|---|---|---|
| Título da aba | Simulador de Espera do Pronto-Socorro | Simulador de Espera da UPA |
| 1 · título | Simulador de espera do pronto-socorro | Simulador de espera da UPA |
| 1 · subtítulo | pacientes de um pronto-socorro | pacientes de uma UPA |
| 1 · notas | Simulador de Espera do Pronto-Socorro | Simulador de Espera da UPA |
| 2 · título | Quem chega ao pronto-socorro não sabe quanto vai esperar | Quem chega à UPA não sabe quanto vai esperar |
| 2 · cartão | Gestores do hospital | Gestores da UPA |
| 2 · notas | esperou horas num pronto-socorro | esperou horas numa UPA |
| 3 · notas | pulseira colorida no pronto-socorro | pulseira colorida na UPA |
| 4 · causa 1 | Casos leves lotam o pronto-socorro: … 64,5% dos que foram direto ao PS não eram urgentes. | Casos leves lotam a UPA: … 64,5% dos que foram direto à urgência não eram urgentes. |
| 4 · causa 2 | Faltam leitos e profissionais para tanta demanda. | Faltam profissionais e vagas para internar quem precisa. |
| 4 · notas | vai direto ao pronto-socorro … direto ao PS … Faltam leitos e profissionais. | vai direto à UPA … direto à urgência … Faltam profissionais, e quem precisa ser internado fica esperando vaga em um hospital. |
| 5 · título | E se o hospital pudesse ver, em segundos, … | E se a UPA pudesse ver, em segundos, … |
| 5 · notas | dar ao hospital um número claro | dar à UPA um número claro |
| 6 · rodapé | quem coordena o pronto-socorro | quem coordena a UPA |
| 8 · rodapé | github.com/Arthur2080/sistema_filas_hospitalares | github.com/Arthur2080/sistema_filas_upa |
| 12 · notas | o hospital passa a enxergar a espera | a UPA passa a enxergar a espera |

No slide 4, "leitos" saiu porque a UPA não interna pacientes: quem precisa de internação é transferido para
um hospital e muitas vezes fica esperando vaga. Pelo mesmo motivo, o dado de 64,5% passou a dizer
"direto à urgência", já que o estudo original fala de pronto-socorro.

### Repositório

| O quê | Antes | Depois |
|---|---|---|
| Nome no GitHub | `Arthur2080/sistema_filas_hospitalares` | `Arthur2080/sistema_filas_upa` |
| Remoto `origin` do git | `https://github.com/Arthur2080/sistema_filas_hospitalares.git` | `https://github.com/Arthur2080/sistema_filas_upa.git` |

O endereço antigo continua funcionando: o GitHub redireciona para o novo. Quem já tem o projeto clonado pode
atualizar o remoto com `git remote set-url origin https://github.com/Arthur2080/sistema_filas_upa.git`.

## O que ficou igual de propósito

- **Nomes das filas** (Emergência, Principal e Fast Track): aguardando decisão da equipe (veja abaixo).
- **Cálculos, tempos máximos do Protocolo de Manchester, faixas de espera e diagrama do banco (slide 10)**:
  valem igual para a UPA.
- **"Plantão"**: a UPA também funciona em plantões de 24 horas.

## Pendências

1. **Nomes das filas.** Fast Track é comum em pronto-socorro de hospital grande. Na UPA, o caminho costuma
   ser sala vermelha (estabilização) e depois consultório médico. Se a equipe decidir trocar os nomes, todos
   estes pontos precisam mudar juntos. Senão a fila aparece com zero pacientes e o gráfico de rosca fica
   sem cor:
   - `backend/ProtocoloManchester.java`: a fila de cada cor
   - `backend/Simulacao.java`: `getPacientesFastTrack`, o campo `percentualFastTrack` e a lista das filas em `toJson`
   - `frontend/js/app.js`: o cartão "Fast track" e as cores das filas em `mostrarGraficoFilas` (ligadas pelo nome)
   - `frontend/index.html`: os textos dos botões de cor
   - `backend/TesteEstatistica.java`: os testes de fila
   - `README.md`: as tabelas de indicadores, gráficos e regras de negócio
   - Slide 1 (animação) e slide 3 (tabela)
2. **Cor azul.** Algumas UPAs encaminham o paciente azul para a UBS em vez de atendê-lo. Se a UPA de
   referência fizer isso, o prazo de 240 min e a faixa "240 min ou mais" precisam ser revistos.
3. **Fontes do slide 4.** Conferir se os estudos citados (Saber Digital, 2019; Bittencourt e Hortale, 2009)
   servem para UPA ou se é melhor usar dados de UPAs.
4. **Nome da pasta no computador.** A pasta local ainda se chama `sistema_filas_hospitalares`. Dá para
   renomear à vontade (de preferência com o editor fechado); o git não depende do nome da pasta.
5. **Slide editado direto no HTML.** As mudanças foram feitas no arquivo exportado. Se o slide for exportado
   de novo pela ferramenta original, elas se perdem: é preciso repetir as trocas lá.
