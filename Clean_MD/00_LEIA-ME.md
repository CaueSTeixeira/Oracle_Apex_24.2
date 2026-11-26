# Documentação APEX 24.2 em Markdown (extraída de CaueSTeixeira/Oracle_Apex_24.2)

Origem: HTML oficial da Oracle (APEX 24.2). Convertido para Markdown limpo (sem menus/imagens/links internos).
Tokens estimados = caracteres / 4 (aproximação).

## Camada 1 — carregar SEMPRE no projeto (~4,7 mil tokens)
- 00_indice_apex_api.md  — pacotes APEX_* e nomes de todos os subprogramas (evita inventar API)
- 00_indice_js_api.md    — namespaces apex.* e membros (política: JS só em último caso)

## Camada 2 — carregar como arquivos do projeto (recuperados sob demanda)
| Pasta | Conteúdo | ~Tokens |
|---|---|---|
| api_compacto/ | APEX_UTIL, APEX_APPLICATION, APEX_ERROR, APEX_DEBUG, APEX_COLLECTION, APEX_SESSION, APEX_SESSION_STATE, APEX_STRING, APEX_JSON, APEX_PAGE, APEX_AUTHORIZATION, APEX_ITEM — só descrição, sintaxe, parâmetros e retorno (sem exemplos) | 85 mil |
| app_builder/ | Estado de sessão e itens; processamento de página (processos, validações, computations, branches, condições); Dynamic Actions; Debug; Autorização | 48 mil |
| js_api/ | apex.item, item, apex.page, apex.server, apex.message, apex.da, apex.region, region, apex.util, apex.event, apex.debug, apex.navigation, apex.lang (sem exemplos) | 43 mil |
| release_notes/ | Novidades, mudanças de comportamento, depreciados, problemas conhecidos da 24.2 | 15 mil |

Dica: APEX_UTIL (~31 mil) e APEX_COLLECTION/APEX_JSON/APEX_ITEM são os maiores; se o projeto ficar pesado, suba só os pacotes que o sistema realmente usa.

## Regra de citação
Cada arquivo traz o comentário "Fonte:" com a publicação. Link base: https://docs.oracle.com/en/database/oracle/apex/24.2/
(aeapi = API Reference, htmdb = App Builder, aexjs = JavaScript API, htmrn = Release Notes)

## Fora do pacote (de propósito)
SQL Workshop, Administration, End User, Installation, Licensing, Accessibility; exemplos de código; Oracle Database 19c (não faz parte do repositório).
