<template>
  <div class="swap-container">
    <swap-confirmation-modal/>

    <div class="title-block">
      <interface-container-title :title="$t('common.swap')"/>
      <div class="buy-eth">
        <span>Buy ETH with</span>
        <img :src="images.visaMaster">
      </div>
    </div>

    <div class="send-form">
      <div class="form-block amount-to-address">
        <div class="amount">
          <div class="title">
            <h4>{{ $t('common.from') }}</h4>
          </div>
          <currency-picker
            :currency="fromArray"
            :token="true"
            page="SwapContainerFrom"/>
          <div class="the-form amount-number">
            <input
              type="number"
              name=""
              value=""
              placeholder="Deposit Amount" >
          </div>
        </div>
        <div class="exchange-icon">
          <img :src="images.swap">
        </div>
        <div class="amount">
          <div class="title">
            <h4>{{ $t('common.to') }}</h4>
          </div>
          <currency-picker
            :currency="toArray"
            :token="true"
            page="SwapContainerTo"/>
          <div class="the-form amount-number">
            <input
              type="number"
              name=""
              value=""
              placeholder="Received Amount" >
          </div>
        </div>
      </div>
    </div>

    <div class="send-form">
      <div class="title-container">
        <div class="title title-and-copy">
          <h4>{{ $t('common.toAddress') }}</h4>
          <p class="copy-button prevent-user-select">Copy</p>
        </div>
      </div>
      <div class="the-form gas-amount">
        <drop-down-address-selector/>
      </div>
    </div>

    <div class="send-form">
      <div class="title-container">
        <div class="title title-and-copy">
          <h4>Providers</h4>
        </div>
      </div>
      <providers-radio-selector/>
    </div>

    <div
      v-if="false"
      class="send-form">
      <div class="title-container">
        <div class="title">
          <div class="title-and-popover">
            <h4>{{ $t('common.speedTx') }}</h4>
            <popover :popcontent="$t('popover.whatIsSpeedOfTX')"/>
          </div>
          <p>{{ $t('common.txFee') }}: 0.000013 ETH ($1.234)</p>
        </div>
        <div class="buttons">
          <div class="small-circle-button-green-border">
            {{ $t('common.slow') }}
          </div>
          <div class="small-circle-button-green-border active">
            {{ $t('common.regular') }}
          </div>
          <div class="small-circle-button-green-border">
            {{ $t('common.fast') }}
          </div>
        </div>
      </div>

      <div class="the-form gas-amount">
        <input
          type="number"
          name=""
          value=""
          placeholder="Gas Amount" >
        <div class="good-button-container">
          <p>Gwei</p>
          <i
            class="fa fa-check-circle good-button not-good"
            aria-hidden="true"/>
        </div>
      </div>
    </div>

    <div class="submit-button-container">
      <h4 v-if="false">1 ETH = 0.000231 BTC</h4>
      <div
        class="submit-button large-round-button-green-filled clickable"
        @click="swapConfirmationModalOpen">
        {{ $t('common.continue') }}
        <i
          class="fa fa-long-arrow-right"
          aria-hidden="true"/>
      </div>
    </div>

  </div>
</template>
<script>
import ProvidersRadioSelector from '../../components/ProvidersRadioSelector';
import CurrencyPicker from '../../components/CurrencyPicker';
import DropDownAddressSelector from '@/components/DropDownAddressSelector';
import InterfaceBottomText from '@/components/InterfaceBottomText';
import InterfaceContainerTitle from '../../components/InterfaceContainerTitle';
import swapIcon from '@/assets/images/icons/swap.svg';
import ImageKybernetowrk from '@/assets/images/etc/kybernetowrk.png';
import ImageBity from '@/assets/images/etc/bity.png';
import ImageVisaMaster from '@/assets/images/etc/visamaster.png';
import SwapConfirmationModal from './components/SwapConfirmationModal';

export default {
  components: {
    'interface-bottom-text': InterfaceBottomText,
    'interface-container-title': InterfaceContainerTitle,
    'currency-picker': CurrencyPicker,
    'drop-down-address-selector': DropDownAddressSelector,
    'providers-radio-selector': ProvidersRadioSelector,
    'swap-confirmation-modal': SwapConfirmationModal
  },
  data() {
    return {
      images: {
        kybernetowrk: ImageKybernetowrk,
        bity: ImageBity,
        visaMaster: ImageVisaMaster,
        swap: swapIcon
      },
      toArray: [
        { symbol: 'BTC', name: 'Bitcoin' },
        { symbol: 'Aug', name: 'Augur' },
        { symbol: 'OMG', name: 'OhMyGod' }
      ],
      fromArray: [
        { symbol: 'BTC', name: 'Bitcoin' },
        { symbol: 'Aug', name: 'Augur' },
        { symbol: 'OMG', name: 'OhMyGod' }
      ]
    };
  },
  methods: {
    swapConfirmationModalOpen() {
      this.$children[0].$refs.swapconfirmation.show();
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'SwapContainer.scss';
</style>
