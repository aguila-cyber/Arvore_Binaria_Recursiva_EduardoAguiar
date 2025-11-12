# 🌳 Trabalho Prático – Árvores Binárias e Recursividade

**Disciplina:** Estrutura de Dados  
**Tema:** Árvores Binárias e uso de Recursividade  
**IDE:** Eclipse  
**Entrega:** via Repositório GitHub  

---

## 📚 Parte 1 — Conceitos Teóricos

### 🌀 O que é Recursividade?
Recursividade é uma técnica de programação onde uma função chama a si mesma para resolver partes menores de um mesmo problema.  
Ela é muito usada em estruturas como árvores, listas e algoritmos de busca.

**Exemplo simples:**
```java
int fatorial(int n) {
    if (n == 0) return 1;  // caso base
    return n * fatorial(n - 1); // chamada recursiva
}

🌲 Recursividade nas Árvores Binárias

Em uma árvore binária, cada subárvore também é uma árvore.
Isso torna a recursão ideal para percorrer e manipular seus nós.

Exemplo (em ordem):

void emOrdem(Node no) {
    if (no == null) return;
    emOrdem(no.esquerda);
    System.out.print(no.valor + " ");
    emOrdem(no.direita);
}

Implementação

O projeto foi implementado em Java (Eclipse) com três classes principais:
src/
 ├── Node.java
 ├── ArvoreBinaria.java
 └── Main.java

Node.java
public class Node {
    int valor;
    Node esquerda;
    Node direita;

    public Node(int valor) {
        this.valor = valor;
        this.esquerda = null;
        this.direita = null;
    }

    @Override
    public String toString() {
        return String.valueOf(valor);
    }
}

ArvoreBinaria.java
import java.util.ArrayList;
import java.util.List;

public class ArvoreBinaria {
    private Node raiz;

    public ArvoreBinaria() {
        this.raiz = null;
    }

    public void inserir(int valor) {
        raiz = inserirRec(raiz, valor);
    }

    private Node inserirRec(Node atual, int valor) {
        if (atual == null) return new Node(valor);
        if (valor < atual.valor) atual.esquerda = inserirRec(atual.esquerda, valor);
        else if (valor > atual.valor) atual.direita = inserirRec(atual.direita, valor);
        return atual;
    }

    public boolean buscar(int valor) {
        return buscarRec(raiz, valor);
    }

    private boolean buscarRec(Node atual, int valor) {
        if (atual == null) return false;
        if (valor == atual.valor) return true;
        return valor < atual.valor ? buscarRec(atual.esquerda, valor) : buscarRec(atual.direita, valor);
    }

    public List<Integer> preOrdem() {
        List<Integer> res = new ArrayList<>();
        preOrdemRec(raiz, res);
        return res;
    }

    private void preOrdemRec(Node atual, List<Integer> res) {
        if (atual == null) return;
        res.add(atual.valor);
        preOrdemRec(atual.esquerda, res);
        preOrdemRec(atual.direita, res);
    }

    public List<Integer> emOrdem() {
        List<Integer> res = new ArrayList<>();
        emOrdemRec(raiz, res);
        return res;
    }

    private void emOrdemRec(Node atual, List<Integer> res) {
        if (atual == null) return;
        emOrdemRec(atual.esquerda, res);
        res.add(atual.valor);
        emOrdemRec(atual.direita, res);
    }

    public List<Integer> posOrdem() {
        List<Integer> res = new ArrayList<>();
        posOrdemRec(raiz, res);
        return res;
    }

    private void posOrdemRec(Node atual, List<Integer> res) {
        if (atual == null) return;
        posOrdemRec(atual.esquerda, res);
        posOrdemRec(atual.direita, res);
        res.add(atual.valor);
    }
}


Main.java
import java.util.List;

public class Main {
    public static void main(String[] args) {
        ArvoreBinaria arvore = new ArvoreBinaria();

        int[] valores = {50, 30, 70, 20, 40, 60, 80};
        for (int v : valores) arvore.inserir(v);

        System.out.println("Buscar 40: " + arvore.buscar(40));
        System.out.println("Buscar 25: " + arvore.buscar(25));

        List<Integer> pre = arvore.preOrdem();
        List<Integer> em = arvore.emOrdem();
        List<Integer> pos = arvore.posOrdem();

        System.out.println("Pré-ordem: " + pre);
        System.out.println("Em-ordem: " + em);
        System.out.println("Pós-ordem: " + pos);
    }
}

Saída do Programa
Buscar 40: true
Buscar 25: false
Pré-ordem: [50, 30, 20, 40, 70, 60, 80]
Em-ordem: [20, 30, 40, 50, 60, 70, 80]
Pós-ordem: [20, 40, 30, 60, 80, 70, 50]
