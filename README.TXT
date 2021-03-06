1. О модуле Shoputils.Payeer 2.0.x-2.1.x-2.2.x - v2.3 (Модуль оплаты "Платежная система PAYEER")

  Модуль оплаты "Payeer" позволяет принимать платежи через систему
  Payeer - http://payeer.com/.

  Возможности модуля:
  - Отсроченная (отложенная) оплата;
  - Статус заказа при подтверждении, оплате и отмене заказа;
  - Установка минимальной и максимальной суммы заказа, при которой модуль будет включен;
  - Управление шаблонами e-mail оповещений о результатах оплаты покупателей и администраторов интернет-магазина;
  - Произвольное название метода оплаты на странице оформления заказа;
  - Вывод инструкции по оплате на странице подтверждении заказа;
  - Ведение журнала запросов от сервера "PAYEER";
  - Выбор (установка) валюты PAYEER;
  - Информация по настройке параметров Payeer на закладке "Информация";
  - Совместимость с модулем "Заказ и регистрация Simple"
  
  Посмотреть как работает и настраивается модуль можно по адресу:
  http://opencart.shoputils.ru/demo/20
  http://opencart.shoputils.ru/demo/20/admin/ (Логин: demo, Пароль: demo)
   
2. Установка модуля

   2.1 Распакуйте архив, скопируйте содержимое директории upload в папку с установленным Opencart 2.0.x и нажмите 
     "Активировать" в "Панель администратора" - "Дополнения" - "Оплата" - "Платежная система PAYEER, v2.1"

   2.2 Для корректной работы отсроченной оплаты необходимо установить OCMOD-расширение модуля.
     В "Панель администратора" - "Модули" - "Установка расширений" нажмите кнопку "Загрузить"
     и выберите файл ocmod/ваша_версия_opencart/ocmod_shoputils_payeer_laterpay.ocmod.xml из дистрибутива.
     После появления надписи "Модуль успешно установлен!" необходимо перейти в
     "Панель администратора" - "Модули" - "Модификаторы" и нажать кнопку "Обновить"
     (см. рис. http://opencart.shoputils.ru/image/data/install/rk_install_oc2.0_1.png )
     
   2.3 В "Панель администратора" - "Дополнения" - "Оплата" - "Платежная система PAYEER, v2.0" Нажмите "Редактировать"
     и настройте модуль оплаты для приема платежей через "PAYEER" (см. п.3).
     
   2.4 Модуль имеет отображение иконок оплаты. Чтобы они показывались при выборе методов оплаты на страницах магазина,
     необходимо исправить следующий файл (правку можно пропустить, если она уже существует, если используется движок ocStore версии 2.1.0.2.1
     и выше или если используется модуль "Simple - упрощенная регистрация и заказ"):
     
        Для версий 2.0 - 2.2 - catalog/view/theme/{ваша_тема}/template/checkout/payment_method.tpl
          
          Сразу после блока:
				  
        <?php foreach ($payment_methods as $payment_method) { ?>
        <div class="radio">
          <label>
            <?php if ($payment_method['code'] == $code || !$code) { ?>
            <?php $code = $payment_method['code']; ?>
            <input type="radio" name="payment_method" value="<?php echo $payment_method['code']; ?>" checked="checked" />
            <?php } else { ?>
            <input type="radio" name="payment_method" value="<?php echo $payment_method['code']; ?>" />
            <?php } ?>
            <?php echo $payment_method['title']; ?>
            <?php if ($payment_method['terms']) { ?>
            (<?php echo $payment_method['terms']; ?>)
            <?php } ?>
				  
          Добавить следующие строки:

        <?php //Shoputils Payment Modules Begin ?>
        <?php if (isset($payment_method['description'])) { ?>
        <br /><small><?php echo $payment_method['description']; ?></small>
        <?php } ?>
        <?php //Shoputils Payment Modules End ?>


3. Настройка модуля

  - Статус
	
  - Отображать модуль только залогинненым администраторам
    Если опция включена, то модуль будет доступен при оформлении заказа только администратору, если он залогинен
    в админ-панели. Это удобно, если необходимо не показывать модуль покупателям на время тестирования и настройки.

	- Статус заказа после оплаты
    После успешной оплаты заказа, заказу будет установлен выбранный статус.
	
	- Статус заказа после подтверждения
	  При нажатии на кнопку "Подтвердить" на последнем этапе оформления заказа, заказу будет установлен выбранный статус
   
  - Статус заказа после неудачной оплаты.
    Если Payeer вернет покупателя после неудачного платежа, заказу будет установлен выбранный статус.
    
  - Статус заказа для отсроченной оплаты.
    После проверки заказа менеджер магазина выставит данный статус, покупатель будет уведомлен по e-mail и сможет оплатить заказ.
    Также, ссылка на оплату появится в личном кабинете покупателя в разделе "Мои заказы".
    БУДЬТЕ ВНИМАТЕЛЬНЫ!
    Если данный статус будет совпадать со "статус заказа после подтверждения" - режим отсроченной оплаты будет отключен и покупатели
    будут перенаправляться на сайт "Единой Кассы" для оплаты сразу после нажатия на кнопку "Оформить заказ".
    
  - Режим отсроченной оплаты.
    При включенном режиме отсроченной (отложенной) оплаты покупатель сможет оплатить заказ только после проверки заказа менеджером магазина.
    Если Вам необходимо, чтобы у покупателя была возможность произвести оплату сразу после оформления заказа без подтверждения менеджером -
    не включайте эту опцию.

  - Название.
    Название метода оплаты на странице оформления заказа.
    ВНИМАНИЕ!!! Для Opencart/ocStore v1.5.1.3 и ниже есть ограничение: не переименовывайте название метода оплаты, если включена отсроченная
    оплата и в системе присутствуют не оплаченные отсроченные заказы. В противном случае, покупатели, не успевшие оплатить отсроченные заказы,
    никогда не смогут их оплатить.
    
  - Инструкция по оплате.
    Инструкция по оплате выводится при подтверждении заказа. Если поле не заполнено - инструкция по оплате выводиться не будет.

  - Отображать иконку "Оплатить заказ" в ЛК покупателя, если оплата заказа прервана.
    Как это работает? Покупатель перешел на сайт платежной системы и не стал оплачивать заказ (передумал, не хватило денег,
    отключили электричество в доме или офисе и пр.). Тогда в его Личном Кабинете (ЛК) в списке истории заказов появится иконка "$",
    нажав на которую покупатель сможет снова попробовать оплатить свой заказ. Иконка появится только в том случае, если текущий статус
    заказа покупателя совпадает со статусом заказа, указанных в полях "Статус заказа после подтверждения" и "Статус заказа после неудачной оплаты".
    
  - Текст кнопки button_confirm ("Потвердить заказ").
    Кнопка выводится на последнем этапе оформления заказа. При нажатии на нее заказ будет сформирован окончательно и покупатель будет отправлен
    для оплаты на сайт платежной системы (если режим отсроченной оплаты отключен).
    
  - Свой шаблон письма покупателю об успешной оплате.
    Если включено - после успешной оплаты покупателю на e-mail придет письмо, шаблон которого можно настроить ниже.
    Если выключено - будет отправляться стандартное в Opencart письмо об изменении заказа.
    Поддерживаются переменные FastTemplate.

  - Свой шаблон письма покупателю о неудачной оплате.
    Если включено - при неудачной оплате покупателю на e-mail придет письмо, шаблон которого можно настроить ниже.
    Если выключено - будет отправляться стандартное в Opencart письмо об изменении заказа.
    Поддерживается переменные FastTemplate.

  - Отправлять администратору уведомление по e-mail об успешной оплате.
    Если включено - администратору и менеджерам ИМ будет отправляться уведомление по e-mail об успешной оплате клиентом. Дополнительные
    e-mail адреса для оповещений Вы можете добавить в "Система->Настройки->Изменить->вкладка "Почта".
    Поддерживается переменные FastTemplate.

  - Отправлять администратору уведомление по e-mail о неудачной оплате.
    Если включено - администратору и менеджерам ИМ будет отправляться уведомление по e-mail о неудачной оплате клиентом.
    Дополнительные e-mail адреса для оповещений Вы можете добавить в "Система->Настройки->Изменить->вкладка "Почта"
    Поддерживается FastTemplate.

    Список возможных значений FastTemplate:
    № заказа - {order_id}
    Название магазина	- {store_name}
    Логотип магазина - {logo}
    Список купленных товаров - {products}
    Итого - {total}
    Имя Отчество покупателя - {customer_firstname}
    Фамилия покупателя - {customer_lastname}
    Группа покупателя - {customer_group}
    e-mail покупателя - {customer_email}
    Телефон покупателя - {customer_telephone}
    Статус заказа - {order_status}
    Комментарий покупателя к заказу - {comment}
    IP адрес покупателя - {ip}
    Дата добавления заказа - {date_added}
    Дата изменения заказа - {date_modified}

  - Идентификатор магазина (ID)
    Идентификатор магазина зарегистрированного в системе «PAYEER». 
    Узнать его можно в аккаунте Payeer: "Аккаунт -> Магазин -> Настройки".
    Пример: 3111827
	
  - Секретный ключ
    Секретный ключ оповещения о выполнении платежа, который используется для проверки целостности полученной информации и однозначной идентификации отправителя.
    Должен совпадать с секретным ключем, указанным в аккаунте Payeer: "Аккаунт -> Магазин -> Настройки".
    Пример: iUqJPrkQkdbECTH5.
	
  - Валюта магазина
    Валюта, в которой магазин передает сумму платежа на платежный 
    шлюз "Payeer"
	
  - Журнал:
  - Журнал запросов от Payeer сохраняется в файле: system/logs/shoputils_payeer.log
  
    В аккаунте Payeer ("Аккаунт -> Магазин -> Настройки") необходимо указать следующие URL: 
    URL успешной оплаты;
    URL неуспешной оплаты;
    URL обработчика;
    Их значения указаны в настройках модуля (Административная панель -> Дополнения -> Оплата -> Платежная система Payeer -> вкладка "Информация").
    БУДЬТЕ ВНИМАТЕЛЬНЫ!!! При "копи-пасте" в браузере, следите, чтобы не было лишних пробелов в начале или конце URL`ов!
          
(с) Shoputils ( http://opencart.shoputils.ru ) 2010 - 2016
     