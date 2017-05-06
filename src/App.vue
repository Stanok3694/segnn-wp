<template>
  <div id="app">

<!--navbar-->
    <div class="navbar-wrapper">
      <div class="container">
        <nav class="navbar navbar-inverse navbar-static-top">
          <div class="container">
            <div class="navbar-header">
              <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
                <span class="icon-bar"></span>
              </button>
              <a class="navbar-brand" >СтройЭлектроГрупп</a>
            </div>
            <div id="navbar" class="navbar-collapse collapse">
              <ul class="nav navbar-nav">
                <li class="active" ><a href="#" @click="resetContentAndHeaders">Главная</a></li>
                <li><a href="#portfolio" @click="togglePortfolioVisible">Наше портфолио</a></li>
                <li><a href="#contacts" @click="toggleContactsVisible">Контакты</a></li>
              </ul>
            </div>
          </div>
        </nav>
      </div>
    </div>
    <!--end of navbar-->

<!--carousel-->
    <carousel></carousel>
<!--marketing-->
    <div class="container marketing" v-if="isFeaturesBlockVisible">
      <!-- features-togglers-->
      <div class="row">
        <!--first toggler-->
        <feature-toggler
          :toggler="firstTogglerType">
        </feature-toggler>  
        <!--end of first toggler-->

        <!--first toggler-->
        <feature-toggler
          :toggler="secondTogglerType">
        </feature-toggler>  
        <!--end of first toggler-->

        <!--first toggler-->
        <feature-toggler
          :toggler="thirdTogglerType">
        </feature-toggler>  
        <!--end of first toggler-->

      </div><!-- /.row -->
      <!--features-->

      <div class="row featurette" id="feature">
        <!-- feature-content-component -->
        <feature-content 
            :visibility="isFirstFeatureVisible"
            :feature="firstTypeOfFeature"
            :header = "firstFeatureHeader"
            :content="firstFeatureContent"
            :divider="isFirstDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isFirstImageVisible"
            :source="firstFeatureImage"
            :feature="firstTypeOfImage">
        </feature-image>
      </div>

      <div class="row featurette">
        <!-- feature-content-component -->
        <feature-content
            :visibility="isSecondFeatureVisible"
            :feature="secondTypeOfFeature"
            :header = "secondFeatureHeader"
            :content="secondFeatureContent"
            :divider="isSecondDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isSecondImageVisible"
            :source="secondFeatureImage"
            :feature="secondTypeOfImage">
        </feature-image>
      </div>

      <div class="row featurette">
        <!-- feature-content-component -->
        <feature-content
            :visibility="isThirdFeatureVisible"
            :feature="firstTypeOfFeature"
            :header = "thirdFeatureHeader"
            :content="thirdFeatureContent"
            :divider="isThirdDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isThirdImageVisible"
            :source="thirdFeatureImage"
            :feature="firstTypeOfImage">
        </feature-image>
      </div>
    </div>
    <!--end of marketing-->

<!--portfolio-->
    <div id="portfolio" v-if="isProjectsVisible">
      <hr class="featurette-divider">
      <h2 align="center">Наши проектные работы</h2>
      <div class="wrapper">
        <div class="col-md-3" id="card" v-for="project in projects">
          <p>{{project.owner}}</p>
          <p>{{project.name}}</p>
          <p>{{project.data}}</p>
        </div>
      </div>
      <hr class="featurette-divider">
      <h2 align="center">Наши электромонтажные работы</h2>
      <div class="wrapper">
        <div class="col-md-3 card" v-for="wiring in wirings">
          <p>{{wiring.owner}}</p>
          <p>{{wiring.name}}</p>
          <p>{{wiring.data}}</p>
        </div>
      </div>
      <hr class="featurette-divider">
      <h2 align="center">Наши энергетические обследования</h2>
      <div class="wrapper">
        <div class="col-md-3 card" v-for="audit in energoAudit">
          <p>{{audit.owner}}</p>
          <p>{{audit.name}}</p>
          <p>{{audit.data}}</p>
        </div>
      </div>
    </div>
    <!--end of portfolio-->
<!--contacts-->
    <div id="contacts" class="wrapper" v-if="isContactsVisible">
      <div class="row">
        <!--first toggler-->
        <contact-type
          :feature="featureToggleType"
          :header="firstContactHeader"
          :content="firstContactContent"
          :source="firstContactImage">
        </contact-type>  
        <!--end of first toggler-->

        <!--first toggler-->
        <contact-type
          :feature="featureToggleType"
          :header="secondContactHeader"
          :content="secondContactContent"
          :source="secondContactImage">
        </contact-type>  
        <!--end of first toggler-->

        <!--first toggler-->
        <contact-type
          :feature="featureToggleType"
          :header="thirdContactHeader"
          :content="thirdContactContent"
          :source="thirdContactImage">
        </contact-type>  
        <!--end of first toggler-->

      </div><!-- /.row -->
    </div>
    <!--end of contacts-->
<!-- footer-custom-component -->
      <my-footer />
      <!--end of footer-->
  </div>
</template>

<script>

import myFooter from '../src/components/Footer.vue';
import FeatureContent from '../src/components/FeatureContent.vue';
import FeatureImage from '../src/components/FeatureImage.vue';
import FeatureToggler from '../src/components/FeatureToggler.vue';
import ContactType from '../src/components/ContactType.vue';
import Carousel from '../src/components/Carousel.vue';
import axios from 'axios';

export default {
  name: 'app',
  data () {
     return {
    // our-portfolio contents data
            projects: {
                firstProject:{
                    owner: 'ОАО «Мобильные Теле Системы»',
                    name: 'Внешнее электроснабжение БССС №52204, г.Арзамас, ул. 9 мая, д.25',
                    data: 'Воздушно-кабельная линия 0,4кВ длиной 450м'
                },
                secondProject:{
                    owner: 'ЗАО «Ойкумена»',
                    name: 'Электроснабжение жилого комплекса «Гагаринские высоты» по пр. Гагарина в р-не НГСХА',
                    data: 'Кабельная линия 6 кВ от ПС 110/6кВ «Мыза» длиной 3050м'
                },
                thirdProject:{
                    owner: 'ОАО «Тульские городские электрические сети»',
                    name: 'Проектирование кабеля 6 кВ от ПС№218 "Южная" до РП 41 в Привокзальном районе г.Тулы',
                    data: 'КЛ 6 кВ длиной 2800м,камера КСО- 1 шт., пристрой к РП'
                }
            },
            wirings: {
                firstProject:{
                    owner: 'ООО «Нижегородстрой»',
                    name: 'Физкультурно-оздоровительный комплекс (ФОК) в г. Перевоз',
                    data: 'Наружные и внутренние сети 0,4 кВ. Полный комплекс работ'
                },
                secondProject:{
                    owner: 'ЗАО «МОСМАРТ»',
                    name: 'Электроснабжение ТЦ на ст. Варя, г.Н.Новгород.Внешние сети',
                    data: '4 300 м кабельных линий в земле АСБ 3х240, 4 кабеля'
                },
                thirdProject:{
                    owner: 'ООО «Зефс-Энерго»',
                    name: 'Электроснабжение строительной площадки Метромоста на правом берегу р.Оки',
                    data: 'Кабельная линия в земле длиной 2000 м, АСБ 3х240, 2 кабеля. Двухцепная ВЛЗ проводом СИП3 150 мм² длиной 300 м.'
                }
            },
            energoAudit: {
                firstProject:{
                    owner: 'Подведомственные учреждения,находящиеся в собственности Заказчика, по адресу: Нижегородская область, Перевозский район, с.Б.Кемары, с.Дубское',
                    name: '«Администрация Дубского сельсовета Перевозского муниципального района Нижегородской области», Адрес:Нижегордская область, Перевозский район, с.Дубское, ул.Центральная, д.105А',
                    data: '«Проведение энергетического обследования, составление отчета и разработка комплексной программы по повышению эффективности» и «Разработка энергетического паспорта»'
                },
                secondProject:{
                    owner: 'Подведомственные учреждения, находящиеся в собственности Заказчика, по адресу: Нижегородская область, Перевозский район, с.Танайково, с.Шпилево',
                    name: '«Администрация Танайковского сельсовета Перевозского муниципального района Нижегородской области», Адрес: Нижегордская область, Перевозский район, с.Тилинино, ул.Молодежная, д.13',
                    data: '«Проведениеэнергетическогообследования, составлениеотчета и разработкакомплексной программыпо повышениюэффективности» и«Разработкаэнергетического паспорта»'
                },
                thirdProject:{
                    owner: 'Подведомственное учреждение Управления образования администрации Перевозского муниципального района Нижегородской области по адресу: Нижегородская область, Перевозский район, с. Тилинино, ул. Новая, д.12',
                    name: 'МДОУ «Детский сад «Жемчужинка» по адресу: Нижегородская область, Перевозский район, с. Тилинино, ул. Новая, д.12',
                    data: '«Проведение энергетического обследования, составление отчета и разработка комплексной программы по повышению эффективности» и «Разработка энергетического паспорта»'
                }
            },
    // feature-toggler headers data
            firstTogglerHeader: 'Электромонтажные работы',
            secondTogglerHeader: 'Энергоаудит',
            thirdTogglerHeader: 'Специальные виды работ',
    // feature-toggler contents data
            firstTogglerContent: 'Основное направление деятельности СтройЭлектроГрупп. ' 
                         + 'Оказываем полный комплекс услуг по электромонтажу.',
            secondTogglerContent: 'Предварительный энергоаудит или энергоаудит, как отдельная услуга? ' 
                         + 'Это не важно. Для Вас мы готовы провести глубокое исследование в сфере ' 
                         + 'аудита энергосетей.',
            thirdTogglerContent: 'Работы любого уровня сложности. Сложные комплексные проекты или сложные операции. ' 
                         + 'В сфере электромонтажых работ для СтройЭлектроГрупп нет ничего невозможного.',
    // feature-toggler type
            firstTogglerType: 'first',
            secondTogglerType: 'second',
            thirdTogglerType: 'third',
    // feature-content headers default data  
            firstFeatureHeader: 'Качество',
            secondFeatureHeader: 'Опыт',
            thirdFeatureHeader: 'Гибкость',
    // feature-content contents default data
            firstFeatureContent: 'Ключевой критерий для нас - качество выполняемых работ. ' 
                         + 'Проводником нашего стремления к максимальному качеству стал комплекс '
                         + 'современных технологий, талантливых рабочих и грамотного взаимодействия '
                         + 'с нашими клиентами. Мы знаем как сделать КАЧЕСТВЕННО',
            secondFeatureContent: 'Вот уже более 15 лет СтройЭлектроГрупп осуществляет свою деятельность. ' 
                         + 'Пройденный нами путь способствовал достижению высокого уровня зрелости бизнес-процессов '
                         + 'как внутри компании, так и во взаимодействии с клиентами. '
                         + 'с нашими клиентами. Мы знаем КАК делать',
            thirdFeatureContent: 'Благодаря стремлению к новым интересным задачам, ' 
                         + 'наша компания накопила значительный багаж самых разных проектов. '
                         + 'Это позволяет нам браться за любые профильные задачи и решать их в соответствии с Вашими ожиданиями. '
                         + 'Мы знаем ЧЕГО ВЫ ХОТИТЕ',
    // feature-images default URLs
            firstFeatureImage: 'src/assets/images/features/default/default1.jpg',
            secondFeatureImage: 'src/assets/images/features/default/default2.jpg',
            thirdFeatureImage: 'src/assets/images/features/default/default3.jpg',
    // feature-toggler images urls
            firstAvatarImage: 'src/assets/images/avatars/avatar1.jpg',
            secondAvatarImage: 'src/assets/images/avatars/avatar2.jpg',
            thirdAvatarImage: 'src/assets/images/avatars/avatar3.jpg',
    // classes data
                firstTypeOfFeature: 'col-md-7',
                secondTypeOfFeature: 'col-md-7 col-md-push-5',
                firstTypeOfImage: 'col-md-5',
                secondTypeOfImage: 'col-md-5 col-md-pull-7',
                featureToggleType: 'col-lg-4 col-md-4 feature-toggler', 
    // flags
            isFirstFeatureVisible: true,
            isSecondFeatureVisible: true,
            isThirdFeatureVisible: true,
            
            isFirstDividerVisible: true,
            isSecondDividerVisible: true,
            isThirdDividerVisible: true,
            isContactDividerVisible: false,
            
            isFirstImageVisible: true,
            isSecondImageVisible: true,
            isThirdImageVisible: true,

            isTogglerBlockVisible: true,
            isProjectsVisible: false,
            isContactsVisible: false,
            isFeaturesBlockVisible: true,
    // data object for header
            featureHeaders: {
                // for "ГЛАВНАЯ" feature-content components
                defaultFeatureHeaders: {
                    firstDefaultHeader: 'Качество',
                    secondDefaultHeader: 'Опыт',
                    thirdDefaultHeader: 'Гибкость'
                },
                // for "ЭЛЕКТРОМОНТАЖНЫЕ РАБОТЫ" feature-content components
                wiringFeatureHeaders:{
                    firstHeader: 'Производство электромонтажных работ',
                    secondHeader: 'Бестраншейная прокладка коммуникаций',
                    thirdHeader: 'Пусконаладочные работы'
                },
                // for "ЭНЕРГОАУДИТ" feature-content components
                energoAuditFeatureHeaders:{
                    firstHeader: 'Анализ',
                    secondHeader: 'Отчёт'
                },                
                // for "ЭНЕРГОАУДИТ" feature-content components
                specialWorksFeatureHeaders:{
                    firstHeader: 'Ремонт',
                    secondHeader: 'Монтаж'
                }
            },
    // data object for content
            featureContents:{
                defaultTexts: {
                    firstText: 'Ключевой критерий для нас - качество выполняемых работ. ' 
                         + 'Проводником нашего стремления к максимальному качеству стал комплекс '
                         + 'современных технологий, талантливых рабочих и грамотного взаимодействия '
                         + 'с нашими клиентами. Мы знаем как сделать КАЧЕСТВЕННО',
                    secondText: 'Вот уже более 15 лет СтройЭлектроГрупп осуществляет свою деятельность. ' 
                         + 'Пройденный нами путь способствовал достижению высокого уровня зрелости бизнес-процессов '
                         + 'как внутри компании, так и во взаимодействии с клиентами. '
                         + 'с нашими клиентами. Мы знаем КАК делать',
                    thirdText: 'Благодаря стремлению к новым интересным задачам, ' 
                         + 'наша компания накопила значительный багаж самых разных проектов. '
                         + 'Это позволяет нам браться за любые профильные задачи и решать их в соответствии с Вашими ожиданиями. '
                         + 'Мы знаем ЧЕГО ВЫ ХОТИТЕ'
                },
                wiringFeatureTexts:{
                    firstText: 'ООО "СтройЭлектроГрупп" оказывает полный комплекс услуг по монтажу, '
                         + 'наладке и организации электроснабжения на объектах энергетической '
                         + 'отрасли, в производственных, складских, торговых, офисных зданиях и '
                         + 'сооружениях, а также прочих объектах недвижимости.',
                    secondText: 'Одной из услуг оказываемых ООО СтройЭлектроГрупп» является '
                         + 'бестраншейная прокладка коммуникаций путём прокола. '
                         + 'Для работы не требуется стационарных источников энергии и воды '
                         + 'Бурение осуществляется за счет продавливания и последующего расширения '
                         + 'и уплотнения грунта.'
                         + 'Главной особенностью является то, что работа производится из котлована.',
                    thirdText: 'Пусконаладочные работы, сопровождающие электромонтажные работы, '
                         + 'представляют собой комплекс работ, включающий проверку, настройку '
                         + 'и испытания электрооборудования с целью обеспечения его проектных '
                         + 'параметров и режимов.',
                },
                energoAuditFeatureTexts:{
                    firstText: 'Энергетическое обследование или энергоаудит проводится ' 
                         + 'и как отдельная процедура, и как составляющая проекта по ' 
                         + 'электромонтажу. В рамках энергоаудита наши сотрудники проводят '
                         + 'все необходимые анализы из возможных и самостоятельно оценивают результаты.',
                    secondText: 'По результатам измерений и последующих расчётов ' 
                         + 'исполненных во время проведения энергоаудита составляются отчёты. ' 
                         + 'Руководствуясь результатами обследования и данными в отчёте рекомендациями '
                         + 'можно успешно реализовывать работы по электромонтажу.'
                },
                specialWorksFeatureTexts:{
                    firstText: 'Специалисты ООО «СтройЭлектроГрупп» имеют опыт проведения '
                         + 'специальных видов работ. Одним из примеров подобных работ является '
                         + 'Монтаж 4-х мачт оповещения ПМЖ 22,8 на объектах инженерной защиты ' 
                         + 'Макарьево-Желтоводского монастыря Лысковского района, Нижегородской области.',
                    secondText: 'Другим примером работы особой сложности является ' 
                         + 'Ремонт ввода ВЛ-35кВ. ТП35/0,4 ФКУ «Исправительная колония №6 ГУФСИН '
                         + 'России по Нижегородской области. '
                }
            },
    // data object for images
            featureImages: {
                defaultImages: {
                    firstImage: 'src/assets/images/features/default/default1.jpg',
                    secondImage: 'src/assets/images/features/default/default2.jpg',
                    thirdImage: 'src/assets/images/features/default/default3.jpg'
                },
                wiringFeatureImages: {
                    firstImage: 'src/assets/images/features/wiring/wiring1.jpg',
                    secondImage: 'src/assets/images/features/wiring/wiring2.jpg',
                    thirdImage: 'src/assets/images/features/wiring/wiring3.jpg'
                },
                energoAuditFeatureImages: {
                    firstImage: 'src/assets/images/features/audit/audit2.jpg',
                    secondImage: 'src/assets/images/features/audit/audit3.jpg'
                },
                specialWorksFeatureImages: {
                    firstImage: 'src/assets/images/features/special/special1.png',
                    secondImage: 'src/assets/images/features/special/special2.png'
                    }
            },
    // contacts headers:
            firstContactHeader: 'Мы ждём Ваших звонков',
            secondContactHeader: 'Мы ждём Ваших писем',
            thirdContactHeader: 'Мы ждём Вас',
    // contacts contents:
            firstContactContent: 'Наш сотовый: 8-800-555-35-35',
            secondContactContent: 'Наш e-mail: prokol@pro.col',
            thirdContactContent: 'Наш адрес: г.Нижний Новгород, ул. Лескова, д.37',
    // contacts images:
            firstContactImage: 'src/assets/images/contacts/phone.png',
            secondContactImage: 'src/assets/images/contacts/email.png',
            thirdContactImage: 'src/assets/images/contacts/road.png'
    }
  },
  methods: {
        
    // trigges for setting data in feature-content components
        firstFeatureBlock: function() {
            this.setFeatureContent('feature-one');
            this.setFeatureHeader('feature-one');
            this.setFeatureImage('feature-one');
            this.toggleFeatureContentBlockVisibility('feature-one');
        },
        secondFeatureBlock: function() {
            this.setFeatureContent('feature-two');
            this.setFeatureHeader('feature-two');
            this.setFeatureImage('feature-two');
            this.toggleFeatureContentBlockVisibility('feature-two');
        },
        thirdFeatureBlock: function() {
            this.setFeatureContent('feature-three');
            this.setFeatureHeader('feature-three');
            this.setFeatureImage('feature-three');
            this.toggleFeatureContentBlockVisibility('feature-three');
        },
        resetContentAndHeaders: function(){
            this.isProjectsVisible = false;
            this.isContactsVisible = false;
            this.isFeaturesBlockVisible = true;

            this.setVisible();
            this.setDefaultData();
        },
    // setters for feature-content and feature-image components DEFAULT data
        setDefaultData: function(){
            this.setDefaultFeaturesContents();
            this.setDefaultFeaturesHeaders();
            this.setDefaultFeaturesImages();
        },
        setDefaultFeaturesContents: function(){
            this.firstFeatureContent = this.featureContents.defaultTexts.firstText;
            this.secondFeatureContent = this.featureContents.defaultTexts.secondText;
            this.thirdFeatureContent = this.featureContents.defaultTexts.thirdText;
        },
        setDefaultFeaturesHeaders: function(){
            this.firstFeatureHeader = this.featureHeaders.defaultFeatureHeaders.firstDefaultHeader;
            this.secondFeatureHeader = this.featureHeaders.defaultFeatureHeaders.secondDefaultHeader;
            this.thirdFeatureHeader = this.featureHeaders.defaultFeatureHeaders.thirdDefaultHeader;
        },
        setDefaultFeaturesImages: function(){
            this.firstFeatureImage = this.featureImages.defaultImages.firstImage;
            this.secondFeatureImage = this.featureImages.defaultImages.secondImage;
            this.thirdFeatureImage = this.featureImages.defaultImages.thirdImage;
        },
    // setters for feature-content and feature-image components ACTUAL data
        setFeatureHeader: function(name){
            if(name == "feature-one"){
                this.firstFeatureHeader = this.featureHeaders.wiringFeatureHeaders.firstHeader;
                this.secondFeatureHeader = this.featureHeaders.wiringFeatureHeaders.secondHeader;
                this.thirdFeatureHeader = this.featureHeaders.wiringFeatureHeaders.thirdHeader;
            }
            if(name == "feature-two"){
                this.firstFeatureHeader = this.featureHeaders.energoAuditFeatureHeaders.firstHeader;
                this.secondFeatureHeader = this.featureHeaders.energoAuditFeatureHeaders.secondHeader;
            }
            if(name == "feature-three"){
                this.firstFeatureHeader = this.featureHeaders.specialWorksFeatureHeaders.firstHeader;
                this.secondFeatureHeader = this.featureHeaders.specialWorksFeatureHeaders.secondHeader;
            }
        },
        // should change this method for real data
        setFeatureContent: function(name){
            if(name == "feature-one"){
                this.firstFeatureContent = this.featureContents.wiringFeatureTexts.firstText;
                this.secondFeatureContent = this.featureContents.wiringFeatureTexts.secondText;
                this.thirdFeatureContent = this.featureContents.wiringFeatureTexts.thirdText;
            }
            if(name == "feature-two"){
                this.firstFeatureContent = this.featureContents.energoAuditFeatureTexts.firstText;
                this.secondFeatureContent = this.featureContents.energoAuditFeatureTexts.secondText;
            }
            if(name == "feature-three"){
                this.firstFeatureContent = this.featureContents.specialWorksFeatureTexts.firstText;
                this.secondFeatureContent = this.featureContents.specialWorksFeatureTexts.secondText
            }
        },
        setFeatureImage: function(name){
            if(name == "feature-one"){
                this.firstFeatureImage = this.featureImages.wiringFeatureImages.firstImage;
                this.secondFeatureImage = this.featureImages.wiringFeatureImages.secondImage;
                this.thirdFeatureImage = this.featureImages.wiringFeatureImages.thirdImage;
            }
            if(name == "feature-two"){
                this.firstFeatureImage = this.featureImages.energoAuditFeatureImages.firstImage;
                this.secondFeatureImage = this.featureImages.energoAuditFeatureImages.secondImage;
            }
            if(name == "feature-three"){
                this.firstFeatureImage = this.featureImages.specialWorksFeatureImages.firstImage;
                this.secondFeatureImage = this.featureImages.specialWorksFeatureImages.secondImage;
            }
        },
    // visible-unvisible triggers
        toggleContactsVisible: function(){
            this.isContactsVisible = true;
            this.isProjectsVisible = false;
            this.isFeaturesBlockVisible = false;

            this.setFeatureContent('contacts');
        },
        togglePortfolioVisible: function() {
            this.isProjectsVisible = true;
            this.isContactsVisible = false;
            this.isFeaturesBlockVisible = false;
        },
        toggleFeatureContentBlockVisibility: function(name){
            if(name == 'feature-one'){
                this.setVisible();
            }
            if(name == 'feature-two' || name == 'feature-three'){
                this.setInvisible();              
            }
        },
        setVisible: function(){
            this.setVisibleForThirdBlock();
            this.setVisibleForThirdDivider();
        },
        setInvisible: function(){
            this.setInvisibleForThirdBlock();
            this.setInvisibleForThirdDivider(); 
        },
        setVisibleForThirdBlock: function(){
            this.isThirdFeatureVisible = true;
            this.isThirdImageVisible = true;
        },
        setInvisibleForThirdBlock: function(){
            this.isThirdFeatureVisible = false;
            this.isThirdImageVisible = false; 
        },
        setVisibleForThirdDivider: function(){
            this.isThirdDividerVisible = true;
        },
        setInvisibleForThirdDivider: function(){
            this.isThirdDividerVisible = false;
        }
    
  
  },
  components: {
    myFooter: myFooter,
    FeatureContent: FeatureContent,
    FeatureImage: FeatureImage,
    FeatureToggler: FeatureToggler,
    ContactType: ContactType,
    Carousel: Carousel
  },
  created(){
      axios.get('src/assets/data/toggler.json')
        .then(response => {
            this.links = response.data.links;
            })
        .catch(e => {
            console.log('error');
            })
  }
}
</script>