# PHP Snippets

####Modified search with ACF
---
    - Modify functions.php:

     //Join posts and postmeta tables
      function cf_search_join( $join ) {
          global $wpdb;

          if ( is_search() ) {
              $join .=' LEFT JOIN '.$wpdb->postmeta. ' ON '. $wpdb->posts . '.ID = ' . $wpdb->postmeta . '.post_id ';
          }

          return $join;
      }

      //Modify the search query with posts_where
      function cf_search_where( $where ) {
          global $pagenow, $wpdb;

          if ( is_search() ) {
              $where = preg_replace(
                  "/\(\s*".$wpdb->posts.".post_title\s+LIKE\s*(\'[^\']+\')\s*\)/",
                  "(".$wpdb->posts.".post_title LIKE $1) OR (".$wpdb->postmeta.".meta_value LIKE $1)", $where );
          }

          return $where;
      }

      //Prevent duplicates
      function cf_search_distinct( $where ) {
          global $wpdb;

          if ( is_search() ) {
              return "DISTINCT";
          }

          return $where;
      }

      - Use  <?php get_search_form( true ); ?>
      - Include search.php:

      <?php get_header(); ?>

              <section class="module module-search-results">
                  <div class="container">
                  <div class="copy">
                      <h1><?php echo sprintf( __( '%s Search Results for ', 'cisco' ), $wp_query->found_posts ); echo get_search_query(); ?></h1>

                      <?php get_template_part('partials/loop'); ?>

                       <?php get_template_part( 'partials/pagination'); ?>
                  </div>
                  </div>
              </section>

      <?php get_footer(); ?>

      - Include search form.php:

      <form action="<?php echo home_url(); ?>" id="search" method="get">

              <input type="search" name="s" value="" />
              <i class="fa fa-search"></i>
              <input type="submit" class="send fa fa-paper-plane-o" value="&#xf1d9;"/>

      </form>

