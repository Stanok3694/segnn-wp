<template>
  <div id="app">

<!--navbar-->
    <my-navbar></my-navbar>
    <!--end of navbar-->

<!--carousel-->
    <carousel></carousel>
<!--marketing-->
    <div class="container marketing" v-show="isFeaturesBlockVisible">
      <!-- features-togglers-->
      <div class="row">
        <!--first toggler-->
        <feature-toggler
          :toggler="firstElementType">
        </feature-toggler>  
        <!--end of first toggler-->

        <!--first toggler-->
        <feature-toggler
          :toggler="secondElementType">
        </feature-toggler>  
        <!--end of first toggler-->

        <!--first toggler-->
        <feature-toggler
          :toggler="thirdElementType">
        </feature-toggler>  
        <!--end of first toggler-->

      </div><!-- /.row -->
      <!--features-->

      <div class="row featurette" id="feature">
        <!-- feature-content-component -->
        <feature-content 
            :visibility="isFirstFeatureVisible"
            :feature="firstTypeOfFeature"
            :content="firstElementType"
            :divider="isFirstDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isFirstImageVisible"
            :source="firstElementType"
            :feature="firstTypeOfFeature">
        </feature-image>
      </div>

      <div class="row featurette">
        <!-- feature-content-component -->
        <feature-content
            :visibility="isSecondFeatureVisible"
            :feature="secondTypeOfFeature"
            :content="secondElementType"
            :divider="isSecondDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isSecondImageVisible"
            :source="secondElementType"
            :feature="secondTypeOfFeature">
        </feature-image>
      </div>

      <div class="row featurette">
        <!-- feature-content-component -->
        <feature-content
            :visibility="isThirdFeatureVisible"
            :feature="firstTypeOfFeature"
            :content="thirdElementType"
            :divider="isThirdDividerVisible">
        </feature-content>
        <!-- feature-image-component -->
        <feature-image
            :visibility="isThirdImageVisible"
            :source="thirdElementType"
            :feature="firstTypeOfFeature">
        </feature-image>
      </div>
    </div>
    <!--end of marketing-->

<!--portfolio-->
    <div id="portfolio" v-show="isProjectsVisible">
    <!--projects-->
      <projects 
        :content="firstPortfolioDataType">
      </projects>
    <!--wirings-->
      <projects
        :content="secondPortfolioDataType">
      </projects>
    <!--audit-->
      <projects
        :content="thirdPortfolioDataType">
      </projects>
    </div>
    <!--end of portfolio-->
<!--contacts-->
    <div id="contacts" class="wrapper" v-show="isContactsVisible">
      <div class="row">
        <!--first contact-->
        <contact-type
          :content="firstElementType">
        </contact-type>  
        <!--end of first contact-->

        <!--second contact-->
        <contact-type
          :content="secondElementType">
        </contact-type>  
        <!--end of second contact-->

        <!--third contact-->
        <contact-type
          :content="thirdElementType">
        </contact-type>  
        <!--end of third contact-->

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
import myNavbar from '../src/components/Navbar.vue';
import FeatureContent from '../src/components/FeatureContent.vue';
import FeatureImage from '../src/components/FeatureImage.vue';
import FeatureToggler from '../src/components/FeatureToggler.vue';
import ContactType from '../src/components/ContactType.vue';
import Carousel from '../src/components/Carousel.vue';
import Projects from '../src/components/Projects.vue';

import axios from 'axios';

export default {
  name: 'app',
  data () {
     return {
    // our-portfolio contents data
            firstPortfolioDataType: 'project',    
            secondPortfolioDataType: 'wiring',    
            thirdPortfolioDataType: 'audit',    
    // feature-toggler and feature-content and feature-images type
            firstElementType: 'first',
            secondElementType: 'second',
            thirdElementType: 'third',
    // feature-content and feature-image type
            firstTypeOfFeature: 'first',
            secondTypeOfFeature: 'second',
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

    }
  },
  methods: {
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
    myNavbar: myNavbar,
    FeatureContent: FeatureContent,
    FeatureImage: FeatureImage,
    FeatureToggler: FeatureToggler,
    ContactType: ContactType,
    Carousel: Carousel,
    Projects: Projects
  }
}
</script>