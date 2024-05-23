# Guia Rápido de TypeScript

Bem-vindo ao guia rápido de TypeScript! Este documento fornece uma visão geral dos conceitos fundamentais do TypeScript, ajudando você a começar a programar com esta linguagem poderosa.

## O que é TypeScript?

TypeScript é um superconjunto de JavaScript desenvolvido pela Microsoft que adiciona tipagem estática opcional à linguagem. Ele compila para JavaScript puro, o que significa que você pode usá-lo em qualquer ambiente que suporte JavaScript.

## Instalação

Para instalar o TypeScript, você precisará do Node.js. Uma vez que o Node.js esteja instalado, você pode instalar o TypeScript globalmente via npm:

```bash
npm install -g typescript
```

## Compilação

Para compilar um arquivo TypeScript (.ts) para JavaScript (.js), use o comando tsc:

```bash
tsc arquivo.ts
```

## Configuração do TypeScript

Você pode configurar seu projeto TypeScript criando um arquivo tsconfig.json na raiz do projeto. Aqui está um exemplo básico:

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"]
}
```

Ou execulte o comando para criar automaticamente o tsconfig.json:

```bash
tsc --init
```

Com o arquivo tsconfig.json instalado, para compilar, use o comando tsc, sem necessidade de especificar o arquivo.

```bash
tsc
```

> Para compilar automaticamente os arquivos TypeScript sempre que houver uma alteração, você pode usar a opção -w (ou --watch) junto com o comando tsc. Isso fará com que o compilador do TypeScript permaneça em modo de observação, monitorando os arquivos do projeto e recompilando-os automaticamente sempre que detectar uma mudança. 

```bash
tsc -w
```

## Tipos Básicos

### Tipos Primitivos

```javascript
let isDone: boolean = false;
let decimal: number = 6;
let color: string = "blue";
```

### Arrays

```javascript
let list: number[] = [1, 2, 3];
let list2: Array<number> = [1, 2, 3];
```

### Tuplas

Tipo especial de array que permite armazenar um conjunto de valores de tipos variados, mas com uma quantidade e ordem fixas. Elas são úteis quando você deseja representar um conjunto de valores que estão logicamente relacionados, mas que podem ser de tipos diferentes.

```javascript
let x: [string, number];
x = ["hello", 10];
```

### Enum

Tipo especial que permite definir um conjunto de constantes nomeadas. Ele é útil para representar um grupo de valores relacionados e facilita a leitura e manutenção do código, associando nomes amigáveis a esses valores.

```javascript
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

### Any

Tipo especial que permite desativar a verificação de tipos. Quando você usa any, está dizendo ao compilador que qualquer tipo é aceitável, permitindo maior flexibilidade no seu código. Esse tipo pode ser útil em situações onde você não conhece o tipo exato dos dados que está manipulando ou está migrando código JavaScript existente para TypeScript

```javascript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false;
```

### Void

É usado para indicar que uma função não retorna um valor. É o oposto do tipo any, pois ele especifica que não há retorno. Esse tipo é comum em funções que executam alguma operação, mas não produzem um valor de retorno, como funções que simplesmente imprimem algo no console.

```javascript
function warnUser(): void {
  console.log("This is my warning message");
}
```

### Interfaces
Interfaces são usadas para definir contratos em seu código, especificando a estrutura esperada de um objeto.


```javascript
interface Person {
  // Declaração de uma assinatura de índice, permitindo que a interface 
  // tenha propriedades adicionais de qualquer tipo com chaves que são strings.
  [key: string]: any,
  // Declaração de uma propriedade opcional chamada 'id' que, se presente, deve ser um número.
  id?: number,
  firstName: string;
  lastName: string;
}

function greet(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "John", lastName: "Doe" };
console.log(greet(user));
```

### Classes

Classes em TypeScript são semelhantes às classes em outras linguagens orientadas a objetos.

```javascript
class Animal {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  public move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

let cat = new Animal("Cat");
cat.move(10);
```

Exemplo de um objeto desativando a verificação de tipos para essa variável. Isso permite que você adicione qualquer propriedade ao objeto sem que o TypeScript produza erros.

```javascript
//Exemplo de objeto sem a declaração 
cont obj: any = {}
obj.a = 1000
```

## Modulos
Os módulos ajudam a organizar o código dividindo-o em arquivos e pastas menores.

### Exportar

```javascript
export class Calculator {
  static add(a: number, b: number): number {
    return a + b;
  }
}
```

### Importar

```javascript
import { Calculator } from './Calculator';

let result = Calculator.add(2, 3);
console.log(result); // 5
```

---

## Extras

### Inferência e Anotações de Tipos

#### Inferência de Tipos

A inferência de tipos é um recurso poderoso do TypeScript que permite ao compilador deduzir automaticamente o tipo de uma variável com base no valor atribuído a ela. Isso significa que você não precisa explicitamente declarar o tipo da variável, pois o TypeScript pode inferir esse tipo a partir do contexto. Vejamos um exemplo:

```javascript
let numero = 42; // TypeScript inferirá que 'numero' é do tipo number
```

Neste exemplo, o TypeScript inferiu que numero é do tipo number porque foi inicializado com um valor numérico. Isso é útil porque reduz a necessidade de escrever código redundante e torna o código mais conciso.


#### Anotações de Tipos
As anotações de tipos, por outro lado, são declarações explícitas de tipos em TypeScript. Você pode usar anotações de tipos para definir o tipo de uma variável, parâmetro de função, valor de retorno de função ou qualquer outra estrutura de dados em seu código. Vejamos um exemplo de anotação de tipo:

```javascript
let numero: number = 42; // Aqui, estamos explicitamente dizendo ao TypeScript que 'numero' é do tipo number
```

Neste exemplo, estamos usando uma anotação de tipo (: number) para declarar explicitamente que numero é do tipo number. Embora a inferência de tipos seja poderosa, há momentos em que você pode querer ser mais explícito sobre os tipos em seu código, especialmente em situações onde a inferência pode não ser óbvia ou quando você deseja fornecer mais clareza ao leitor do seu código.

#### Quando Usar Cada Um
- Inferência de Tipos: Use inferência de tipos quando o tipo da variável for óbvio a partir do valor atribuído a ela ou quando você quiser código mais conciso e menos verboso.
- Anotações de Tipos: Use anotações de tipos quando desejar fornecer clareza adicional sobre os tipos em seu código, quando a inferência de tipos não for suficiente ou quando desejar especificar tipos em lugares onde não há valores iniciais para inferência.

#### Benefícios e Considerações
- A inferência de tipos torna o código mais limpo e conciso, enquanto as anotações de tipos fornecem clareza adicional.
- As anotações de tipos podem ser úteis em situações onde a inferência de tipos pode não funcionar conforme o esperado, como em casos de tipos complexos ou ambíguos.
- Usar uma combinação de inferência de tipos e anotações de tipos pode ajudar a equilibrar a concisão e a clareza do código.

## Conclusão

TypeScript é uma ferramenta poderosa que traz tipagem estática e outros recursos avançados para o JavaScript. Este guia rápido cobre apenas os conceitos básicos, mas há muito mais para explorar. Consulte a documentação oficial do TypeScript para mais informações.

