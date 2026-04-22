# Notion Automation — Pipeline Pós-Pesquisa

## Visão Geral

Após concluir qualquer pesquisa /last30days, o pipeline executa automaticamente
dois estágios adicionais:

1. **Salva o resultado** na página Web Research do Notion
2. **Gera um lead magnet** e salva no database Lead Magnets

Ambos os estágios são obrigatórios. Nunca entregue apenas o output no terminal
sem executar os dois estágios.

---

## IDs do Notion (André Rodrigues — A4 Solutions)

| Recurso | ID |
|---------|-----|
| Web Research (página pai) | `34a9530494f4808baeecf6d112d7ead8` |
| Lead Magnets (data source) | `b54e7490-a85a-452f-8748-2f84fb7c761f` |

---

## Estágio A — Salvar Pesquisa no Notion

### Quando executar
Imediatamente após a síntese do /last30days, antes de gerar o lead magnet.

### Nome da subpágina
Padrão obrigatório: `<Assunto Resumido> | AAAAMMDD`

Exemplos:
- `Wearable SST Brasil | 20260422`
- `NR-12 Segurança Máquinas | 20260501`
- `IoT Prevenção Acidentes | 20260515`

O assunto deve ser curto (máximo 4-5 palavras), em português, descritivo do tema pesquisado.
A data é a data atual no formato AAAAMMDD.

### Estrutura da subpágina

```markdown
## Metadados
- **Query:** [query exata usada]
- **Data:** [AAAA-MM-DD]
- **Skill:** last30days v[versão]
- **Fontes ativas:** [lista de fontes que retornaram dados]

---

## O que foi aprendido
[Conteúdo do "What I learned" do output — parágrafos completos]

---

## Key Patterns
[Lista numerada dos KEY PATTERNS do output]

---

## Dados de Engajamento
[Tabela com dados do rodapé: Reddit threads/upvotes, TikTok views/likes, etc.]

---

## Oportunidades Identificadas
[3-5 oportunidades de conteúdo derivadas da análise]
- Post de autoridade: [sugestão]
- Lead magnet: [sugestão de tema]
- Ângulo contrário: [frase provocadora]

---

## Arquivo Raw
Salvo localmente em: [caminho do arquivo raw]
```

### Como criar via Notion MCP
Use a ferramenta `notion-create-pages` com:
- `parent.page_id`: `34a9530494f4808baeecf6d112d7ead8`
- `properties.title`: nome no padrão `Assunto | AAAAMMDD`
- `content`: conteúdo completo conforme estrutura acima

---

## Estágio B — Gerar Lead Magnet

### Quando executar
Imediatamente após salvar a pesquisa no Notion (Estágio A).

### O que gerar
Com base nos insights da pesquisa, gere automaticamente:

**1. Playbook (conteúdo principal)**
- 1.200 a 1.500 palavras
- Linguagem simples — nível médio, sem jargão técnico de SST
- Orientado por narrativa, não por lista
- Estrutura: abertura com contexto → problema → solução → como começar → fechamento com identidade do André
- Sempre incluir no final: *"André Rodrigues — Co-fundador da A4 Solutions, empresa brasileira de IoT para segurança industrial. Passamos 5 anos desenvolvendo tecnologia para os setores de siderurgia, mineração e química."*

**2. Post Contrário**
- Desafia o senso comum do mercado
- Começa com afirmação polêmica
- Termina com chamada para comentar uma palavra-chave para receber o playbook
- Máximo 150 palavras

**3. Post Dor**
- Fala diretamente com a frustração do profissional de SST
- Cenário de risco que o profissional reconhece
- Termina com chamada para comentar uma palavra-chave para receber o playbook
- Máximo 150 palavras

**4. Post Resultado**
- Mostra transformação possível (antes/depois)
- Tom de evidência, não de promessa
- Termina com chamada para comentar uma palavra-chave para receber o playbook
- Máximo 150 palavras

### Regras de tom de voz
Sempre consultar ANDRE-CONTEXT.md antes de gerar qualquer conteúdo.
O lead magnet deve soar como André — não como IA genérica.

### Como salvar via Notion MCP
Use a ferramenta `notion-create-pages` com:
- `parent.data_source_id`: `b54e7490-a85a-452f-8748-2f84fb7c761f`
- Propriedades obrigatórias:

| Campo Notion | Valor |
|-------------|-------|
| Nome | Título do lead magnet |
| Status | `Rascunho` |
| Tipo | `Playbook` (ou tipo adequado) |
| Tema | Tema central em uma frase |
| Fonte da Pesquisa | Nome da subpágina criada no Estágio A |
| Post Contrário | Texto do post contrário |
| Post Dor | Texto do post de dor |
| Post Resultado | Texto do post de resultado |
| date:Data de Criação:start | Data atual no formato YYYY-MM-DD |
| date:Data de Criação:is_datetime | 0 |

- `content`: playbook completo em markdown

---

## Fluxo Completo

```
/last30days [tema]
     ↓
[Síntese do output — exibida no terminal]
     ↓
[Estágio A] Criar subpágina em Web Research
Padrão: "Assunto | AAAAMMDD"
     ↓
[Estágio B] Gerar lead magnet e salvar no database
Status inicial: Rascunho
     ↓
[Confirmação final]
"✅ Pesquisa salva: [link Notion]"
"✅ Lead magnet criado: [link Notion]"
"📋 Próximo passo: revisar o lead magnet e escolher qual post publicar primeiro"
```

---

## Mensagem de Confirmação Final

Após completar os dois estágios, exibir sempre:

```
---
📦 Pipeline concluído:
✅ Pesquisa salva no Notion → [nome da subpágina]
✅ Lead magnet criado → [título do lead magnet]
📋 Status: Rascunho — revisar antes de publicar
🎯 Próximo passo: abrir o lead magnet no Notion, revisar o tom e escolher qual
   dos 3 posts publicar primeiro no LinkedIn
---
```

---

## Tratamento de Erros

Se o Notion MCP não estiver disponível:
- Exibir o output da pesquisa normalmente no terminal
- Exibir o lead magnet gerado no terminal
- Avisar: "⚠️ Notion MCP indisponível. Copie o conteúdo acima e salve manualmente."

Se a pesquisa não retornar dados suficientes para gerar lead magnet:
- Salvar a pesquisa no Notion normalmente
- No campo Lead Magnet, registrar: "Dados insuficientes — repetir pesquisa com query diferente"
- Sugerir 3 queries alternativas para o usuário testar
