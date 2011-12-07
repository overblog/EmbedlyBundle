Introduction
------------
OverblogEmbedlyBundle is a simple Symfony bundle that provides access
to the embed.ly php library (https://github.com/embedly/embedly-php)

See http://embed.ly for more information

Installation
------------

  1. Add this bundle and the embedly-php library to your ``vendor/`` dir:
      * Using the vendors script.

        Add the following lines in your ``deps`` file::

            [OverblogEmbedlyBundle]
                git=git://github.com/ebuzzing/OverblogEmbedlyBundle.git
                target=/bundles/Overblog/EmbedlyBundle

            [embedly-php]
                git=git://github.com/embedly/embedly-php.git
                target=/embedly-php

        Run the vendors script:

            ./bin/vendors install

      * Using git submodules.

            $ git submodule add git=git://github.com/ebuzzing/OverblogEmbedlyBundle.git vendor/bundles/Overblog/EmbedlyBundle
            $ git submodule add git://github.com/embedly/embedly-php.git vendor/embedly-php

  2. Add the Overblog namespace to your autoloader:

``` php

          // app/autoload.php
          $loader->registerNamespaces(array(
                'Overblog' => __DIR__.'/../vendor/bundles',
                'Embedly'   => __DIR__.'/../vendor/embedly-php/src'
                // your other namespaces
          ));
```

  3. Add this bundle to your application's kernel:

``` php

          // app/ApplicationKernel.php
          public function registerBundles()
          {
              return array(
                  // ...
                  new Overblog\EmbedlyBundle\OverblogEmbedlyBundle(),
                  // ...
              );
          }
```

  4. Configure the `overblog_embedly` service in your config:

``` yaml
    overblog_embedly:
        config:
            key: your_api_key
```


Example
-------

In a controller, do the following:

``` php

        $embedly = $this->get('overblog_embedly');
        $oembedResponse = $embedly->get('http://about.over-blog.com/article-participez-a-la-conception-de-la-prochaine-version-d-overblog-91418456.html');
        /*
            object(stdClass)[1251]
  public 'provider_url' => string 'http://about.over-blog.com/' (length=27)
  public 'description' => string 'Mardi 6 décembre 2011 2 06 /12 /Déc /2011 12:44 Dans les mois à venir, nous allons développer une version complètement nouvelle d'OverBlog. La nouvelle version remplacera l'actuelle plateforme, elle sera plus fonctionnelle, plus simple et vos blogs actuels en bénéficieront automatiquement !' (length=298)
  public 'title' => string 'Participez à la conception de la prochaine version d'OverBlog !' (length=64)
  public 'url' => string 'http://about.over-blog.com/article-participez-a-la-conception-de-la-prochaine-version-d-overblog-91418456.html' (length=110)
  public 'thumbnail_width' => int 439
  public 'thumbnail_url' => string 'http://idata.over-blog.com/0/00/63/43/perenoel.jpg' (length=50)
  public 'version' => string '1.0' (length=3)
  public 'provider_name' => string 'Over-blog' (length=9)
  public 'type' => string 'link' (length=4)
  public 'thumbnail_height' => int 269
        */
```
