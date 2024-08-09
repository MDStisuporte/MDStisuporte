- 👋 Hi, I’m @MDStisuporte
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
MDStisuporte/MDStisuporte is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->


import java.util.Random;
import java.util.Scanner;

public class Jogo {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Tabuleiro tabuleiro = new Tabuleiro();
        Jogador jogador1 = new Jogador("Jogador 1");
        Jogador jogador2 = new Jogador("Jogador 2");

        while (true) {
            System.out.println(tabuleiro);
            tabuleiro.moveJogador(jogador1);
            if (tabuleiro.checaVitoria(jogador1)) {
                System.out.println("Parabéns, " + jogador1.getNome() + "! Você ganhou!");
                break;
            }

            System.out.println(tabuleiro);
            tabuleiro.moveJogador(jogador2);
            if (tabuleiro.checaVitoria(jogador2)) {
                System.out.println("Parabéns, " + jogador2.getNome() + "! Você ganhou!");
                break;
            }
        }
        scanner.close();
    }
}

class Tabuleiro {
    private static final int TAMANHO = 10;
    private int[] tabuleiro;
    private Random random;

    public Tabuleiro() {
        tabuleiro = new int[TAMANHO];
        random = new Random();
        // Inicializa o tabuleiro com flores (1-3 flores por célula)
        for (int i = 0; i < TAMANHO; i++) {
            tabuleiro[i] = random.nextInt(3) + 1;
        }
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < TAMANHO; i++) {
            sb.append("[").append(tabuleiro[i]).append("] ");
        }
        sb.append("\n");
        return sb.toString();
    }

    public void moveJogador(Jogador jogador) {
        Scanner scanner = new Scanner(System.in);
        System.out.println(jogador.getNome() + ", escolha um número de 0 a " + (TAMANHO - 1) + ": ");
        int posicao = scanner.nextInt();
        if (posicao < 0 || posicao >= TAMANHO) {
            System.out.println("Número inválido. Tente novamente.");
            return;
        }

        jogador.coletarFlores(tabuleiro[posicao]);
        tabuleiro[posicao] = 0; // Flores coletadas, a célula fica vazia
    }

    public boolean checaVitoria(Jogador jogador) {
        return jogador.getFlores() >= 10; // O jogador precisa de 10 flores para vencer
    }
}

class Jogador {
    private String nome;
    private int flores;

    public Jogador(String nome) {
        this.nome = nome;
        this.flores = 0;
    }

    public String getNome() {
        return nome;
    }

    public int getFlores() {
        return flores;
    }

    public void coletarFlores(int quantidade) {
        this.flores += quantidade;
        System.out.println(nome + " coletou " + quantidade + " flores. Total: " + flores);
    }
}