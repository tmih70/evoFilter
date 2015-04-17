evoFilter
=========
https://github.com/vanchelo/evoFilter

Установка:
скопировать все
==========assets/libs/========================
filter.class.php	(его тоже можно положить в папку libs, хотя в дистрибутиве лежит в assets/snippets/evoFilter/filter.snippet.php, только поменять пути в плагине и сниппете надо)
helpers.php
container.class.php
php_fast_cache.php
=============плагин evoFilter=================
из файла	assets/snippets/evoFilter/filter.plugin.php
==========сниппет evoFilter====================
из файла	assets/snippets/evoFilter/filter.snippet.php
==============чанки для пагинации=====================
 - они обязательны (или надо удалить из filter.class.php в районе 110 строки)
 
чанк	dlnext
<a href="[+link+]"  class="ditto_next_link">[+next+]&nbsp;&nbsp;>></a>
чанк	dlprev
<a href="[+link+]" class='ditto_previous_link'> <<[+prev+]&nbsp;&nbsp;</a>
чанк	dlpage
<a href="[+link+]" class="ditto_page">[+num+]</a>
чанк	dlcurpage
<a href="[+link+]" class="ditto_currentpage">[+num+]</a>
чанк	dlwrappag
<div class="pagination-ditto">[+wrap+]</div>

=============Вызов на странице================= 
есть и такой	
[[evoFilter? &parent=`[*id*]` &tpl=`DlTplGKS-list` &form_tpl=`formTplDL-list3gks` &tvList=`photos, ... price_ed` &display=`3`]]
[[evoFilter? &parent=`4` &tpl=`DLpost` &form_tpl=`new_filter_form2` &only_form=`1`]]
&parent=`4` - конкретная рубрика, из которой вызываем
&only_form=`1` - без результатов вывода
==========
[[evoFilter? &form_tpl=`new_filter_form_alt`]]
<div class="center-col-cont">
    <h2 class="light">Поиск по каталогу городской недвижимости</h2>
	[+ef.form+]   
</div>

Найдено <b>[+ef.items_show_count+]</b> объявлений из <b>[+ef.items_count+]</b> 

<div class="doc-lister">
    [+pages+]
    [+ef.result+]
    [+pages+]
</div>
=====================
Чанк DLpost (пример)
===========DLpost===============
<div class="catalog-item">
 <div class="catalog-item-a">
	  [!if? &is=`[+tv.image-cat+]:empty` &then=`<img src="css3/pix-plus3.png" class="img-cat-item" alt="без картинки" title="без картинки"/>` 
	  &else=`<img src="[!phpthumb? &input=`[!ddGetMF? &string=`[+tv.image-cat+]` &totalRows=`1`!]` &options=`w=116,h=116,zc=1`!]" class="img-cat-item" alt="с фото" title="с фото" style="width:108px; height:108px;"/>` !]
		<h2>[+tv.kind+]</h2>
		<h3>[+pagetitle+]</h3>
		Комнат: [+tv.komnat+] 
		 </div>
		 <div class="catalog-item-b">
		[[truncate? &text=[+introtext+] &len=100]]
		  </div>

		 <div class="catalog-pr-item">
		<font>[!NumFormat? &field=`[+tv.price+]`!]
		 [+tv.price_ed+]</font>&nbsp;&nbsp;&nbsp; <!-- : num_format -->
		 </div>
		  <div class="catalog-item-c">
		<input type="checkbox" name="compare" id="compare[+id+]" value="1" onclick="return shkCompare.toCompare([+id+],[+parent+],this)" [+id:compare=`checked="checked"`+] /><label for="compare[+id+]">Сравнить</label>

		<a title="[+pagetitle+]" href="[~[+id+]~]" class="float-r">Подробнее</a>
  </div>
</div>
=====================
Чанки форм:
=========new_filter_form_alt=====================
<div class="container1">
    <form name="af" method="get" action="[+action+]">

        <div class="block-af"><span class="light">Расположение</span><br>
            <select onchange="location=this.value" class="styled">
                <option value="">выбрать</option>
                [+categories+]
            </select>
        </div>

        <div class="block-af"><span class="light">Тип недвижимости</span><br>
            <select name="[+request_prefix+]28" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":28,"type":"select"}+]
            </select>
        </div>

        <div class="block-af2">
            <input type="checkbox" name="[+request_prefix+]30" value="checked" class="styled" [+tv:{"id":30,"type":"checkbox"}+]><span class="light">Аренда</span>
        </div>

        <div class="block-af"><span class="light">Выберите регион</span><br>
            <select name="[+request_prefix+]20" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":20,"type":"select"}+]
            </select>
        </div>

        <div class="block-af">
            <span class="light">Количество комнат</span><br>
            <select name="[+request_prefix+]17" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":17,"type":"select"}+]
            </select>
        </div>

        <div class="block-af2">
            <input type="checkbox" name="[+request_prefix+]27" value="checked" class="styled" [+tv:{"id":27,"type":"checkbox"}+]><span class="light">С фото</span>
        </div>

        <div class="block-af"><span class="light">Выберите район СПб</span><br>
            <select name="[+request_prefix+]12" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":12,"type":"select"}+]
            </select>
        </div>

        <div class="block-af"><span class="light">Тип дома</span><br>
            <select name="[+request_prefix+]14" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":14,"type":"select"}+]
            </select>
        </div>

        <div class="block-af"><span class="light">Выберите район ЛО</span><br>
            <select name="[+request_prefix+]16" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":16,"type":"select"}+]
            </select>
        </div>

        <div class="block-af">
            <span class="light">Цена менее</span><br>
            <input type="text" name="[+request_prefix+]8" value="[+tv:{"id":8,"type":"num","sign":"<"}+]" class="inp-af">
        </div>

        <input type="submit" class="input-af" value="НАЙТИ">
    </form>
</div>
=============new_filter_form=================
<div class="container1">
    <form name="af" method="get" action="[+action+]" enctype="text/plain">

        <div class="block-af"><span class="light">Расположение</span><br>
            <select onchange="location=this.value" class="styled">
                <option value="">выбрать</option>
                [+categories+]
            </select>
        </div>

        <div class="block-af"><span class="light">Тип недвижимости</span><br>
            <select name="[+request_prefix+]28" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":28,"type":"select"}+]
            </select>
        </div>

        <div class="block-af2">
            <input type="checkbox" name="[+request_prefix+]30" value="checked" class="styled" [+tv:{"id":30,"type":"checkbox"}+]><span class="light">Аренда</span>
        </div>

        <div class="block-af"><span class="light">Выберите страну</span><br>
            <select name="[+request_prefix+]12" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":12,"type":"select"}+]
            </select>
        </div>

        <div class="block-af">
            <span class="light">Количество комнат</span><br>
            <select name="[+request_prefix+]17" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":17,"type":"select"}+]
            </select>
        </div>

        <div class="block-af2">
            <input type="checkbox" name="[+request_prefix+]27" value="checked" class="styled" [+tv:{"id":27,"type":"checkbox"}+]><span class="light">С фото</span>
        </div>

        <div class="block-af"><span class="light">Тип дома</span><br>
            <select name="[+request_prefix+]14" class="styled">
                <option value="">Не задано</option>
                [+tv:{"id":14,"type":"select"}+]
            </select>
        </div>

        <div class="block-af">
            <span class="light">Цена от</span><br>
			<input type="text" name="[+request_prefix+]8[from]" value="[+tv:{"id":8,"type":"price","order":"from"}+]" class="inp-af">
        </div>
		
		<div class="block-af">
            <span class="light">Цена до</span><br>
			<input type="text" name="[+request_prefix+]8[to]" value="[+tv:{"id":8,"type":"price","order":"to"}+]" class="inp-af">
        </div>

        <input type="submit" class="input-af" value="НАЙТИ">
    </form>
</div>
==============================
кнопка СБРОСИТЬ можно так
<input type="reset" class="float-l" name="reset" id="reset" value="СБРОСИТЬ" onclick="window.location.href='[*alias*]'">
==============================
