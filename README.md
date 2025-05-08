import java.util.Scanner;


public class SA {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int numVendedores;
        String[] nomes;
        double[][] vendas;
        double[] totalVendas;
        String[] classificacao;
        double[] bonus;
        double maiorVenda = 0;
        String melhorVendedor = "";
        double valorMelhorVenda = 0;

        System.out.print("Informe o número de vendedores: ");
        numVendedores = scanner.nextInt();

        nomes = new String[numVendedores];
        vendas = new double[numVendedores][5];
        totalVendas = new double[numVendedores];
        classificacao = new String[numVendedores];
        bonus = new double[numVendedores];

       
        for (int i = 0; i < numVendedores; i++) {
            System.out.print("Informe o nome do vendedor " + (i + 1) + ": ");
            nomes[i] = scanner.next();
        }

        System.out.println("Registre as vendas dos 5 dias úteis da semana (segunda a sexta)");

        
        for (int i = 0; i < numVendedores; i++) {
            for (int j = 0; j < 5; j++) {
                System.out.print("Qual o valor das vendas do vendedor " + nomes[i] + " no dia " + (j + 1) + "? ");
                vendas[i][j] = scanner.nextDouble();
                totalVendas[i] += vendas[i][j]; 
            }

           
            if (totalVendas[i] >= 5000) {
                classificacao[i] = "Excelente";
                bonus[i] = 0.10 * totalVendas[i];
            } else if (totalVendas[i] >= 3000) {
                classificacao[i] = "Bom";
                bonus[i] = 0.05 * totalVendas[i];
            } else {
                classificacao[i] = "Regular";
                bonus[i] = 0.0;
            }

            
            if (totalVendas[i] > maiorVenda) {
                maiorVenda = totalVendas[i];
                melhorVendedor = nomes[i];
                valorMelhorVenda = totalVendas[i];
            }
        }

      
        System.out.println("\n============================================================");
        System.out.println("               RELATÓRIO DE VENDAS SEMANAIS                ");
        System.out.println("============================================================");
        System.out.println("| Vendedor         | Total Vendido | Classificação | Bônus     |");
        System.out.println("+----------------------------------------------------------------+");

        for (int i = 0; i < numVendedores; i++) {
            System.out.printf("| %-16s | R$ %11.2f | %-13s | R$ %8.2f |\n",
                    nomes[i], totalVendas[i], classificacao[i], bonus[i]);
        }

        System.out.println("+----------------------------------------------------------------+");
        System.out.printf("MELHOR VENDEDOR DA SEMANA: %s (R$ %.2f)\n", melhorVendedor, valorMelhorVenda);
        System.out.println("============================================================");

        scanner.close();
    }
}
