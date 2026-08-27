# Segurança e qualidade

## Modelo de segurança

O aplicativo utiliza a chave pública apropriada ao cliente. Credenciais privilegiadas e operações de serviço não são embarcadas no frontend.

A autorização é aplicada no PostgreSQL por Row Level Security:

- cada usuário acessa e altera apenas dados permitidos pela própria identidade;
- conteúdo privado não se torna público por conveniência da interface;
- propriedade de registros é validada no banco;
- funções administrativas exigem papel real;
- alterações sensíveis geram rastreabilidade;
- arquivos respeitam proprietário, finalidade e políticas do bucket.

A interface melhora a experiência, mas não é considerada uma barreira de segurança.

## Proteção de dados

- nenhuma credencial ou segredo é versionado;
- arquivos de ambiente ficam fora do Git;
- dados pessoais reais não são usados como seed;
- dados de desenvolvimento, quando necessários, permanecem isolados e identificados;
- exclusões e atualizações respeitam o ciclo de vida do proprietário;
- integrações externas devem registrar origem e condições de uso.

## Evolução do banco

Mudanças estruturais são feitas por migrations SQL ordenadas. O banco pode ser reconstruído de forma reproduzível, evitando alterações manuais invisíveis e divergência entre ambientes.

## Validação registrada

Na última execução completa, em agosto de 2026:

| Verificação | Resultado |
|---|---:|
| Lint do schema PostgreSQL | aprovado |
| Testes de banco e RLS | 229 aprovados |
| Integração de identidade, perfil, Storage e conta | aprovada |
| TypeScript | aprovado |
| Lint do frontend | aprovado |
| Testes automatizados do frontend | 42 aprovados |
| Expo Doctor | 21/21 |
| Exportação web | 52 rotas |

As verificações são executadas sobre a arquitetura real. Contas e dados criados durante validações automatizadas são descartados ao final.
