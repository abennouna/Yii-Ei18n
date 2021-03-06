=========================
Ei18n Module 0.1 Manual 
=========================
Ei18 is a translation module to allow Yii'ers to easily manage missing translations on application pages. 
It is heavily inspired by `yii.translate <https://github.com/gusnips/yii.translate>`_ 
developed by Gustavo Salomé Silva `gusnips <http://www.yiiframework.com/user/6112/>`_.

The module also allows the edition of translations specified by categories. Its utility 
widget WTranslate handles that very smoothly. 

All is AJAX based at the frontend. I thought that would be better to leave to developers 
the creation of a backend in order to edit translation on a regular basis. 

Its Ei18 component has a couple of helper functions to also manage language setting 
automation. Check also its Set CAction class to be included on the controller that will 
handle language setting.


========
Requires
========

    * jQuery v1.7 or higher (tested with jQuery v1.7).
    * `fancybox 2.0.5 <http://fancyapps.com/fancybox/>`_
    * `jwysiwyg 0.97.2 <https://github.com/akzhan/jwysiwyg>`_
    * jbar Jquery plugin -**Modified version**
    * Yii 1.9

===========
Tested with
===========

    * Chrome 17.0.963.56 on Macosx Lion 
    * Safari Version 5.1.3 (7534.53.10) on Macosx Lion
    * Firefox 8.0.1 Macosx Lion
    * Firefox 9.0.1 Macosx Lion

===========
Quick Start
===========

On your main.php config file do the following::

    /* import the module */
        'import'=>array(
        /* ... */
            'application.modules.translate.TranslateModule'
        /* ... */
    /* setup your default language */
	'language'=> 'en',
    /* setup message translation method */
        'components'=>array(
            'messages' => array(
                'class' => 'CDbMessageSource',
                'onMissingTranslation' => array('Ei18n', 'missingTranslation'),
                'sourceMessageTable' => 'tbl_source_message',
                'translatedMessageTable' => 'tbl_message'
            ),
    /* setup global translate application component */
            'translate' => array(
                'class' => 'translate.components.Ei18n',
                'createTranslationTables' => true,
                'connectionID' => 'db',
                'languages' => array(
                    'en' => 'English',
                    'es' => 'Español',
                    'it' => 'Italiano'
                    )
                ),
        ),
    /* setup the module */
        'modules' => array(
            'translate'
        ),
    /* preload the global translate application component */
        'preload'=> array(
            'translate'
        )
        /* ... */

Displaying the editor
--------------------------

Once the module and the translation component have been set. You just use any of 
the following helper functions::

    Yii::app()->translate->renderMissingTranslationsEditor();
    /* or */
    /* Yii::app()->translate->renderTranslationsEditor(array('index','menu')); */


The first method and due to the view rendering nature of Yii, I highly recommend the display of those functions 
at the bottom of your ``main`` or ``base`` layout, as it will collect all missing ones throughout 
the rendering process.
