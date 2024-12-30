 Shortcode WordPress para Posts Fixados

Descrição

Este projeto contém um código PHP para WordPress que cria um shortcode para exibir IDs de posts fixados (sticky posts). Ele é altamente configurável, permitindo controle sobre o índice inicial e o número de posts retornados.

Recursos

Suporte para parâmetros dinâmicos:

result: Total de resultados (personalizável).

index: Índice inicial (começando de 0).

limit: Limita o número de itens retornados.

Ordenação automática dos posts por data de publicação.

Fácil implementação via shortcode no WordPress.

Código Completo

<?php
// Define os posts fixados
function get_fixed_post_shortcode($atts) {
    $atts = shortcode_atts(
        array(
            'result' => '0', // Total de resultados
            'index' => '0', // Índice inicial (0 baseado)
            'limit' => '1', // Limite de itens a serem listados
        ),
        $atts,
        'fixed_posts'
    );

    // Obtém os IDs dos posts fixados
    $sticky = get_option('sticky_posts');

    // Se não houver posts fixos, retorna vazio
    if (empty($sticky)) {
        return '';
    }

    // Ordena os posts fixos por data de publicação, em ordem decrescente
    rsort($sticky);

    // Calcula o índice e o limite
    $index = max(0, (int)$atts['index']);
    $limit = max(1, (int)$atts['limit']);
    $result = array_slice($sticky, $index, $limit);

    // Retorna os resultados como IDs separados por vírgula
    return implode(', ', $result);
}

add_shortcode('fixed_posts', 'get_fixed_post_shortcode');
?>

Uso

Exibir o primeiro post fixado:

[fixed_posts index="0" limit="1"]

Exibir dois posts, pulando o primeiro:

[fixed_posts index="1" limit="2"]

Exibir todos os posts fixados:

[fixed_posts index="0" limit="100"]

Requisitos

WordPress 5.0 ou superior.

Tema ou plugin com suporte a shortcodes.

Instalação

Copie o código para o arquivo functions.php do tema ativo ou adicione em um plugin personalizado.

Salve o arquivo.

Use o shortcode conforme os exemplos acima.

Explicação Técnica

Recebimento de Parâmetros

Define valores padrão e permite substituí-los dinamicamente.

Busca e Ordenação

Obtém os IDs dos posts fixados e os ordena por data.

Filtragem por Índice e Limite

Seleciona os resultados com base nos parâmetros fornecidos.

Saída

Retorna IDs separados por vírgula.
