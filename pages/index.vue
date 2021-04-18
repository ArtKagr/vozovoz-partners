<template>
  <div class="sections">
    <section class="sections-head">
      <h1 class="sections-head-title">Партнеры</h1>
      <h2 class="sections-head-subtitle">Vozovoz</h2>
    </section>
    <section class="sections-procedure">
      <div class="sections-procedure-container">
        <h2 class="sections-procedure-container-title">
          Порядок заключения договора
        </h2>
        <span class="sections-procedure-container-description">
          Заключение договора ООО «Возовоз» с перевозчиками проходит в несколько
          этапов:
        </span>
        <div class="sections-procedure-container-icons">
          <div class="sections-procedure-container-icons-icon">
            <div class="sections-procedure-container-icons-icon-logo">
              <vz-icon-first />
            </div>
            <span class="sections-procedure-container-icons-icon-description">
              Согласование коммерческих<br />
              условий договора
            </span>
          </div>
          <div class="sections-procedure-container-icons-icon">
            <div class="sections-procedure-container-icons-icon-logo">
              <vz-icon-second />
            </div>
            <span class="sections-procedure-container-icons-icon-description">
              Проверка надежности<br />
              перевозчика
            </span>
          </div>
          <div class="sections-procedure-container-icons-icon">
            <div class="sections-procedure-container-icons-icon-logo">
              <vz-icon-third />
            </div>
            <span class="sections-procedure-container-icons-icon-description">
              Согласование договора<br />
              на перевозку с последующим<br />
              доступом в личный кабинет
            </span>
          </div>
        </div>
      </div>
    </section>
    <section class="sections-information">
      <div class="sections-information-container">
        <span class="sections-information-container-description">
          В связи с усилением проводимых Федеральной налоговой службой РФ
          проверок покупателей транспортных услуг и проведением контроля
          выполнения со стороны покупателей проявления должной осмотрительности
          при выборе контрагентов (в рамках исполнения положений Приказа
          Федеральной налоговой службой РФ от 30 мая 2007 года №ММ-3-06/333@ «Об
          утверждении концепции системы планирования выездных налоговых
          проверок», а также позиции Федеральной налоговой службы РФ, изложенной
          в письмах от 23 марта 2017 года №ЕД-5-9/547@ «О выявлении
          обстоятельств необоснованной налоговой выгоды» и от 12 мая 2017 года
          №АС-4-2/8872 «О выявлении фактов ведения налогоплательщиками
          финансово-хозяйственной деятельности с высоким налоговым риском»),
          Общество с ограниченной ответственностью «Возовоз» сообщает, что для
          заключения договоров перевозки грузов нами будут запрошены следующие
          сведения и документы:
        </span>
        <div class="sections-information-container-block">
          <div class="sections-information-container-block-buttons">
            <div
              class="sections-information-container-block-buttons-button"
              :class="activeInformation === 'entities' ? '-active' : ''"
              @click="setActiveButton('entities')"
            >
              <div
                class="sections-information-container-block-buttons-button-icon"
              >
                <vz-icon-personal-active
                  v-if="activeInformation === 'entities'"
                />
                <vz-icon-personal v-else />
              </div>
              <span
                class="sections-information-container-block-buttons-button-title"
              >
                Юридическим<br
                  class="sections-information-container-block-buttons-button-title-break"
                />
                лицам
              </span>
            </div>
            <div
              class="sections-information-container-block-buttons-button"
              :class="activeInformation === 'entrepreneur' ? '-active' : ''"
              @click="setActiveButton('entrepreneur')"
            >
              <div
                class="sections-information-container-block-buttons-button-icon"
              >
                <vz-icon-personal-active
                  v-if="activeInformation === 'entrepreneur'"
                />
                <vz-icon-personal v-else />
              </div>
              <span
                class="sections-information-container-block-buttons-button-title"
                v-text="'Индивидуальным предпринимателям'"
              />
            </div>
          </div>
          <div class="sections-information-container-block-list">
            <div
              v-for="(text, key) in activeInformationData"
              :key="key"
              class="sections-information-container-block-list-item"
            >
              <div class="sections-information-container-block-list-item-point">
                <vz-icon-point />
              </div>
              <span
                class="sections-information-container-block-list-item-text"
                v-text="text"
              />
            </div>
          </div>
        </div>
      </div>
    </section>
    <section v-if="!formData.length" class="sections-form">
      <div class="sections-form-container">
        <h2 class="sections-form-container-title">Форма предложения</h2>
        <div class="sections-form-container-list">
          <div
            v-for="(item, key) in form"
            :key="key"
            class="sections-form-container-list-item"
          >
            <div
              class="sections-form-container-list-item-title"
              :class="[
                item.type === 'radio' ? '-radio' : '',
                item.title === 'Код АТИ (ID)' ? '-info' : '',
              ]"
            >
              <span v-text="item.title" />
              <div
                v-if="item.title === 'Код АТИ (ID)'"
                class="sections-form-container-list-item-title-info"
              >
                <vz-icon-info />
              </div>
            </div>
            <div
              v-if="item.type === 'radio'"
              class="sections-form-container-list-item-radio_container"
            >
              <div
                v-for="(elem, index) in item.values"
                :key="index"
                class="sections-form-container-list-item-radio_container-radio"
                @click="setActiveShippingType(elem.flag)"
              >
                <div
                  class="sections-form-container-list-item-radio_container-radio-button"
                >
                  <vz-icon-radio-active
                    v-if="elem.flag === activeFormRadioButton"
                  />
                  <vz-icon-radio v-else />
                </div>
                <span
                  class="sections-form-container-list-item-radio_container-radio-title"
                  v-text="elem.title"
                />
              </div>
            </div>
            <b-input
              v-else-if="item.type === 'text' || item.type === 'number'"
              v-model="item.value"
              :placeholder="item.placeholder"
              :type="item.type"
              class="sections-form-container-list-item-input"
            />
            <phone-input
              v-else-if="item.type === 'phone'"
              v-model="item.value"
              @set-phone="setPhone($event, key)"
            />
          </div>
        </div>
        <div class="sections-form-container-button_info">
          <b-button
            variant="danger"
            class="sections-form-container-button_info-button"
            pill
            @click="sendFormData"
            v-text="'Отправить предложение'"
          />
          <span class="sections-form-container-button_info-info">
            Нажимая на кнопку "Оформить" вы выражаете свое согласие с
            применяемой<br
              class="sections-form-container-button_info-info-break"
            />
            ООО "Возовоз"
            <a href="#" class="sections-form-container-button_info-info-link">
              политикой в отношении обработки персональных данных.
            </a>
          </span>
        </div>
      </div>
    </section>
    <section v-else class="sections-form_success">
      <div class="sections-form_success-container">
        <div class="sections-form_success-container-icon">
          <vz-icon-success />
        </div>
        <span
          class="sections-form_success-container-title"
          v-text="'Форма предложения отправлена!'"
        />
      </div>
    </section>
    <section class="sections-footer">
      <div class="sections-footer-container">
        <span class="sections-footer-container-description">
          Транспортная компания "Возовоз" организация перевозок грузов<br
            class="sections-footer-container-description-break"
          />
          194292, Санкт-Петербург, 6-й Верхний переулок дом 12 литер А, кабинет
          №210<br class="sections-footer-container-description-break" />
          Телефон: 8 800 707 2002
        </span>
        <div class="sections-footer-container-icons">
          <a
            href="https://www.facebook.com/vozovoz"
            class="sections-footer-container-icons-icon"
          >
            <vz-icon-facebook />
          </a>
          <a
            href="https://vk.com/vozovoz"
            class="sections-footer-container-icons-icon"
          >
            <vz-icon-vk />
          </a>
          <a
            href="https://www.instagram.com/tk.vozovoz"
            class="sections-footer-container-icons-icon"
          >
            <vz-icon-instagram />
          </a>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import VzIconFirst from '../components/icons/vz-icon-first'
import VzIconSecond from '../components/icons/vz-icon-second'
import VzIconThird from '../components/icons/vz-icon-third'
import VzIconPersonal from '../components/icons/vz-icon-personal'
import VzIconPersonalActive from '../components/icons/vz-icon-personal-active'
import VzIconPoint from '../components/icons/vz-icon-point'
import VzIconRadioActive from '../components/icons/vz-icon-radio-active'
import VzIconRadio from '../components/icons/vz-icon-radio'
import VzIconInfo from '../components/icons/vz-icon-info'
import VzIconFacebook from '../components/icons/vz-icon-facebook'
import VzIconVk from '../components/icons/vz-icon-vk'
import VzIconInstagram from '../components/icons/vz-icon-instagram'
import VzIconSuccess from '../components/icons/vz-icon-success'
import PhoneInput from '../components/phoneInput'
export default {
  components: {
    PhoneInput,
    VzIconSuccess,
    VzIconInstagram,
    VzIconVk,
    VzIconFacebook,
    VzIconInfo,
    VzIconRadio,
    VzIconRadioActive,
    VzIconPoint,
    VzIconPersonalActive,
    VzIconPersonal,
    VzIconThird,
    VzIconSecond,
    VzIconFirst,
  },
  data() {
    return {
      activeInformation: 'entities',
      activeFormRadioButton: 'intercity',
      entitiesInformation: [
        'Свидетельство ОГРН и свидетельство ИНН.',
        'Документ, подтверждающий полномочия лица, заключающего сделку (доверенность или протокол/решение об избрании исполнительного органа организации).',
        'Договор аренды офисных помещений контрагента (по юридическому адресу).',
        'Информационное письмо контрагента о фактическом расположении контрагента (если его фактическое расположение отлично от адреса офисных помещений, указанного в договоре аренды по юридическому адресу). Такое письмо готовится контрагентом самостоятельно в свободной форме.',
        'Информационное письмо контрагента о количестве сотрудников (лиц, оформленных в штат) на дату заключения договора. Такое письмо готовится контрагентом самостоятельно в свободной форме.',
        'Выписка из книги продаж (62 счет) за три месяца, предшествующие дате заключения договора, либо Информационное письмо, с указанием контрагентов (покупателей) поставщика, их адресов, ИНН и телефонов. Такое письмо готовится контрагентом самостоятельно в свободной форме.',
        'Декларация по НДС за последний квартал с копией квитанции о приеме декларации налоговым органом в электронном виде.',
        'Информационное письмо контрагента о наличии в собственности, либо в аренде (в том числе в финансовой) или на ином законном основании транспортных средств (с указанием их марок и индивидуализирующих VIN номеров) для оказания услуг по перевозке, либо копий ПТС/СТС таких транспортных средств. Если индивидуальный предприниматель не имеет таких транспортных средств, просим предоставить сведения о фактических перевозчиках, привлекаемых для перевозки грузов ООО «Возовоз», а также копии заключенных с привлекаемыми перевозчиками договоров перевозки грузов. Указанные документы (копии заключенных с привлекаемыми перевозчиками договоров перевозки грузов) должны быть предоставлены в любом случае до момента подачи транспортного средства под погрузку. В случае отсутствия таких документов на момент подачи транспортного средства под погрузку ООО «Возовоз» оставляет за собой право отказать в погрузке транспортного средства с применением к перевозчику ответственности, предусмотренной договором.',
      ],
      entrepreneurInformation: [
        'Свидетельство ИНН и ОГРНИП.',
        'Документ, подтверждающий полномочия лица, совершающего сделку, если фактическим подписантом выступает представитель индивидуального предпринимателя.',
        'Информационное письмо о фактическом расположении контрагента (если его фактическое расположение отлично от адреса государственной регистрации). Такое письмо готовится контрагентом самостоятельно в свободной форме.',
        'Информационное письмо контрагента о количестве сотрудников (лиц, оформленных в штат) на дату заключения договора. Такое письмо готовится контрагентом самостоятельно в свободной форме.',
        'Информационное письмо контрагента о наличии в собственности, либо в аренде (в том числе в финансовой) или на ином законном основании транспортных средств (с указанием их марок и индивидуализирующих VIN номеров) для оказания услуг по перевозке, либо копий ПТС/СТС таких транспортных средств. Если индивидуальный предприниматель не имеет таких транспортных средств, просим предоставить сведения о фактических перевозчиках, привлекаемых для перевозки грузов ООО «Возовоз», а также копии заключенных с привлекаемыми перевозчиками договоров перевозки грузов. Указанные документы (копии заключенных с привлекаемыми перевозчиками договоров перевозки грузов) должны быть предоставлены в любом случае до момента подачи транспортного средства под погрузку. В случае отсутствия таких документов на момент подачи транспортного средства под погрузку ООО «Возовоз» оставляет за собой право отказать в погрузки транспортного средства с применением к перевозчику ответственности, предусмотренной договором.',
      ],
      form: [
        {
          type: 'radio',
          title: 'Перевозки',
          values: [
            { title: 'Междугородние', flag: 'intercity' },
            { title: 'Внутригородские', flag: 'intracity' },
          ],
        },
        {
          type: 'text',
          title: 'Полное название перевозчика',
          placeholder: 'ООО "Везем"',
          value: null,
        },
        {
          type: 'text',
          title: 'ИНН Перевозчика',
          placeholder: '0000 0000 00',
          value: null,
        },
        {
          type: 'text',
          title: 'Юридический адрес перевозчика',
          placeholder: 'Москва, Ленинский проспект 6',
          value: null,
        },
        {
          type: 'text',
          title: 'Фактический адрес перевозчика',
          placeholder: 'Москва, Ленинский проспект 6',
          value: null,
        },
        {
          type: 'number',
          title: 'Количество транспортных средств на балансе',
          placeholder: '25',
          value: null,
        },
        {
          type: 'number',
          title: 'Среднесписочная численность сотрудников',
          placeholder: '10',
          value: null,
        },
        {
          type: 'text',
          title: 'Код АТИ (ID)',
          placeholder: '000 000',
          value: null,
        },
        {
          type: 'text',
          title: 'Сайт перевозчика',
          placeholder: 'vezem.ru',
          value: null,
        },
        {
          type: 'text',
          title: 'ФИО контактного лица',
          placeholder: 'Иванов Иван Иванович',
          value: null,
        },
        {
          type: 'text',
          title: 'Должность контактного лица',
          placeholder: 'Менеджер',
          value: null,
        },
        {
          type: 'phone',
          title: 'Рабочий контактный телефон',
          placeholder: '(###) ### ####',
          value: null,
        },
        {
          type: 'phone',
          title: 'Мобильный контактный телефон',
          placeholder: '(###) ### ####',
          value: null,
        },
        {
          type: 'text',
          title: 'E-mail',
          placeholder: 'Ivanov@vezem.ru',
          value: null,
        },
        {
          type: 'text',
          title: 'Как Вы узнали о нашей компании?',
          placeholder: null,
          value: null,
        },
        {
          type: 'text',
          title: 'Комментарии',
          placeholder: 'Будем рады сотрудничеству!',
          value: null,
        },
      ],
      formData: [],
    }
  },
  computed: {
    activeInformationData() {
      return this.activeInformation === 'entities'
        ? this.entitiesInformation
        : this.entrepreneurInformation
    },
  },
  methods: {
    setActiveButton(flag) {
      this.activeInformation = flag
    },
    setActiveShippingType(flag) {
      this.activeFormRadioButton = flag
    },
    sendFormData() {
      const activeFormRadioButton = this.activeFormRadioButton
      this.formData = this.form.reduce(function (preVal, item) {
        if (item.type === 'radio') {
          preVal.push(activeFormRadioButton)
        } else if (item.value) {
          preVal.push(item.value)
        }
        return preVal
      }, [])
      console.warn('form', this.formData)
    },
    setPhone(phone, key) {
      this.form[key].value = phone
    },
  },
}
</script>
