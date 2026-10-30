# 🐍 OntoSerpentes
---

## 🧑‍💻Desenvolvedores
- Arthur Ricartte: [ArthurRicartte](https://github.com/ArthurRicartte)
- Felipe Coelho: [Friwilly](https://github.com/Friwilly)

## 📌 Sobre o Projeto

O **OntoSerpentes** é uma ontologia desenvolvida no padrão **RDF/RDFS/OWL** voltada para a modelagem semântica, classificação taxonômica da fauna ofídica brasileira. O projeto combina o conhecimento declarativo sobre serpentes, biomas e tipos de dentição com motores de raciocínio dedutivo e consultas SPARQL.

### 🎯 Principais Destaques da Ontologia:
- **12 Classes Hierárquicas:** Organizadas em até 2 níveis de profundidade (ex: `Serpente` → `Peconhenta` → `Viperidae`).
- **11 Propriedades Tipadas:** 5 `ObjectProperty` e 6 `DatatypeProperty` devidamente restritas com `rdfs:domain` e `rdfs:range`.
- **5 Axiomas/Construções OWL:** Modelagem contendo `owl:disjointWith`, `owl:inverseOf`, `owl:SymmetricProperty` e `owl:FunctionalProperty`.
- **27 Instâncias Reais:** Dados de espécies de cobras brasileiras, biomas e dentições.
- **Inferência Semântica (OWL-RL):** Raciocínio lógico automático que expande o conhecimento implícito da base (materializando triplas de simetria, inversão e herança de classes).

---

## 📂 Estrutura do Repositório

```text
sbc-ontologia-cobras/
│── base_cobras.ttl            # Ontologia original em formato Turtle (Axiomas e Instâncias)
│── base_cobras_expandida.ttl  # Base de conhecimento gerada após inferência dedutiva OWL-RL
│── Scripts_Snake_Kb.ipynb     # Jupyter Notebook interativo com todas as etapas e consultas
│── requirements.txt           # Dependências de execução (rdflib, owlrl)
└── README.md                  # Documentação e apresentação do projeto

## 🧬 Estrutura da Ontologia

### 1. Hierarquia de Classes
- **`cobra:Serpente`** (Raiz Principal)
  - **`cobra:Peconhenta`**
    - `cobra:Viperidae`
    - `cobra:Elapidae`
  - **`cobra:NaoPeconhenta`** *(Disjunta de Peconhenta)*
    - `cobra:Boidae`
    - `cobra:Colubridae`
    - `cobra:Aniliidae`
- **`cobra:Bioma`**
  - `cobra:BiomaFlorestal`
  - `cobra:BiomaCampestre`
- **`cobra:TipoDenticao`**

### 2. Axiomas OWL Aplicados
1. **`owl:disjointWith`**: Garante que uma classe não pode sobrepor a outra (`cobra:NaoPeconhenta` vs `cobra:Peconhenta`).
2. **`owl:inverseOf`**: Relaciona bidirecionalmente a habitação do bioma (`cobra:eHabitadoPor` é a inversa de `cobra:habitaBioma`).
3. **`owl:SymmetricProperty`**:
   - `cobra:eSimpatricaCom`: Define coabitação espécies que habitam um mesmo ambiente (Bioma).
   - `cobra:temParenteProximo`: Define simetria taxonômica/evolutiva.
4. **`owl:FunctionalProperty`**: `cobra:nomeCientifico` garante unicidade por espécie.

---

## 💻 Suíte de Consultas e Demonstrações

O notebook `Scripts_Snake_Kb.ipynb` está dividido em 4 partes principais:

1. **Consultas RDFlib Nativas (`g.triples`):** Busca direta por triplas com coringas e filtros.
2. **Consultas SPARQL Avançadas:**
   - `SELECT` com `FILTER`, `ORDER BY` e `LIMIT` (Filtros de risco de acidente, cobras noturnas e tamanhos).
   - Agregações com `GROUP BY` e `COUNT` (Ranking de biomas habitados).
   - Consultas Booleanas (`ASK`) e Hierárquicas (`a/rdfs:subClassOf*`).
   - Regras de inferência via `CONSTRUCT` (Geração de grafo derivado de alertas).
   - Manipulação de dados com `SPARQL UPDATE` (`INSERT DATA`, `DELETE DATA`, `DELETE/INSERT`).
3. **Validação e Testes dos Axiomas OWL:** Testes unitários em SPARQL validando a integridade das regras OWL.
4. **Raciocínio Semântico (`owlrl`):** Expansão do grafo, gerando `base_cobras_expandida.ttl`.

---

## 🚀 Como Executar o Projeto
Basta acessar o Scripts_Snake_Kb.ipynb e executar cada bloco de çodigo !
