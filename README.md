# Aula-05-ES

Exercício Prático — Do Miro ao Python
Contexto
Você vai modelar e implementar um Sistema de Biblioteca Digital (tipo Kindle Unlimited).

# Parte 1: Diagrama no Miro e Draw.io (20 min)

Atores: Leitor, Bibliotecário, Sistema de Pagamento
Monte o diagrama com pelo menos:
✅ 5 casos de uso
✅ 2 relacionamentos <<include>>
✅ 1 relacionamento <<extend>>
✅ Limite do sistema definido

Casos sugeridos:
Buscar livro
Emprestar livro
Devolver livro
Renovar empréstimo
Cadastrar usuário
Aplicar multa (extend de Devolver livro)
Verificar disponibilidade (include de Emprestar livro)

# Parte 2: Especificação (10 min)

Documente o UC: "Emprestar Livro" usando o template:
UC-02: Emprestar Livro
Ator: Leitor
Pré-condições: _______________
Fluxo Principal:
  1. ___
  2. ___
  3. ___
Fluxo de Exceção: _______________
Pós-condições: _______________

# Parte 3: Implementação em Python (30 min)

No Google Colab ou VS Code — sem classes, só listas e dicionários!
💡 Cada bloco de código abaixo representa um Caso de Uso do seu diagrama.

SISTEMA DE BIBLIOTECA DIGITAL — Biblioteca FIAP

Cada seção = um Caso de Uso do diagrama que você fez no Miro

DADOS DO SISTEMA
(imagine como o "banco de dados" por enquanto)

catalogo = [
    {"titulo": "Clean Code",            "autor": "Robert C. Martin", "disponivel": True},
    {"titulo": "The Pragmatic Programmer", "autor": "Hunt & Thomas", "disponivel": True},
    {"titulo": "Design Patterns",       "autor": "Gang of Four",     "disponivel": True},
]
emprestimos = []   # lista de {"leitor": ..., "livro": ...}

UC-01: LISTAR CATÁLOGO
Ator: Leitor

print("📚 Catálogo disponível:")
for livro in catalogo:
    status = "✅" if livro["disponivel"] else "❌"
    print(f"  {status} {livro['titulo']} — {livro['autor']}")

UC-02: BUSCAR LIVRO  ←← complete aqui!
Ator: Leitor
Pré-condição: catálogo não vazio

print("\n🔍 Buscando livro...")
busca = "clean"   # o leitor digitou isso
TODO: percorra o catálogo e imprima apenas os livros
       cujo título contenha o texto da busca (ignore maiúsculas/minúsculas)
       Dica: use  busca.lower() in livro["titulo"].lower()
 --- seu código aqui ---

UC-03: EMPRESTAR LIVRO
Ator: Leitor
<<include>> UC-04 Verificar Disponibilidade

print("\n📌 Empréstimo:")
leitor  = "Ana Silva"
titulo  = "Clean Code"
 <<include>> — verificar disponibilidade (sempre acontece)
livro_encontrado = None
for livro in catalogo:
    if livro["titulo"] == titulo:
        livro_encontrado = livro
        break
if livro_encontrado is None:
    print("❌ Livro não encontrado no catálogo.")
    
elif livro_encontrado["disponivel"] == False:
    # Fluxo de exceção
    print(f"⚠️  '{titulo}' já está emprestado!")
    
else:
    # Fluxo principal
    livro_encontrado["disponivel"] = False
    emprestimos.append({"leitor": leitor, "livro": titulo})
    print(f"✅ '{titulo}' emprestado para {leitor}!")

UC-04: DEVOLVER LIVRO  ←← complete aqui!
Ator: Leitor
 <<extend>> UC-05 Aplicar Multa (só se atrasado)

print("\n🔄 Devolução:")
leitor_devolvendo = "Ana Silva"
titulo_devolvendo = "Clean Code"
 TODO: implemente a devolução seguindo os passos:
   1. Procure na lista `emprestimos` o registro correspondente
   2. Se encontrado: marque o livro como disponivel=True no catálogo
      e remova o registro de `emprestimos`
   3. Se não encontrado: mostre mensagem de erro
   Bônus <<extend>>: pergunte se houve atraso e imprima "📋 Multa aplicada!"
 --- seu código aqui ---

 🔎 ESTADO FINAL — confira o resultado

print("\n📖 Catálogo após operações:")
for livro in catalogo:
    status = "✅" if livro["disponivel"] else "❌"
    print(f"  {status} {livro['titulo']}")
print(f"\n📋 Empréstimos ativos: {emprestimos}")
