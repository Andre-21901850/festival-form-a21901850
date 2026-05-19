# Festival Forms - a21901850

## Alterações e Correções Implementadas

### 1. Ordenação dos dias por data crescente
Na `dias_view` em `views.py`, foi alterado `Dia.objects.all()` para 
`Dia.objects.order_by('data')` de modo a que os dias apareçam ordenados 
cronologicamente na página.

### 2. Formulário de edição de concerto com todos os campos
O `ConcertoForm` em `forms.py` apenas permitia editar o campo `hora`. 
Foi corrigido para incluir todos os campos: `banda`, `dia`, `hora` e `palco`.

### 3. Botão "Apagar concerto"
Adicionado botão de apagar na página de detalhe do concerto (`concerto.html`), 
com um formulário POST e CSRF token. Criada a view `apagar_concerto_view` e 
respetivo URL `concertos/<int:concerto_id>/apagar/`.

### 4. Funcionalidade "Criar concerto"
O link "Criar concerto" no menu não tinha URL nem view. Foi criada a view 
`criar_concerto_view`, o URL `concertos/criar/`, o template `criar_concerto.html` 
e corrigido o `href` no `layout.html`.

### 5. Campo acessibilidade_mobilidade_reduzida no Palco
Adicionado campo booleano `acessibilidade_mobilidade_reduzida` ao modelo `Palco`. 
A página de palcos mostra agora a capacidade, o número total de concertos agendados 
e o símbolo ♿ caso o palco tenha acessibilidade para mobilidade reduzida.

### 6. Editar palco
O botão "Editar palco" na página de palcos não tinha URL associado. Foi criada 
a view `editar_palco_view`, o URL `palcos/<int:palco_id>/editar/` e atualizado 
o `href` no template `palcos.html`. O `PalcoForm` foi também atualizado para 
incluir o novo campo de acessibilidade.

---

## Explicação: ordering = ["dia__data", "hora"]

Esta linha encontra-se na classe `Meta` do modelo `Concerto` e define a ordenação
padrão dos concertos quando são consultados na base de dados.

- `"dia__data"` — ordena pelo campo `data` do modelo `Dia` relacionado (usa `__`
  para atravessar a relação ForeignKey). Os concertos aparecem ordenados por data crescente.
- `"hora"` — dentro do mesmo dia, os concertos são ordenados pela hora de início,
  também de forma crescente.

Sem esta linha, os concertos apareceriam na ordem de inserção na base de dados,
sem qualquer ordenação lógica.