<template>
<a href='https://goo.gl/maps/czfnQnyH7jB2' target='_blank' class="button-map">
	<p class='button-map__text'>{{ $t('buttons.map') }}
		<svg class='button-map__img'>
			<use xlink:href='#arrow-right-up' />
		</svg>
	</p>
    <svg style="display: none">
        <symbol id='arrow-right-up' width="12" height="12" viewBox=" 0 0 24 24">
            <path fill-rule="evenodd" d="M10 6v1.6h5.272L6 16.872 7.128 18 16.4 8.728V14H18V6z" />
        </symbol>
    </svg>
</a>

</template>

<script>

export default {
  name: 'button-map'
}
</script>

<style lang="scss">

.button-map {
    text-decoration: none;
    padding: 1rem 2rem;
    background-color: $BUTTON-COLOR;
    outline: none;
    border: none;
    text-align: center;
    border-radius: 3px;
    @extend %flex-row-c;
    flex-flow: nowrap;
    position: relative;
    z-index: 2;
    @media (max-width: 600px) {
		padding: 1.3rem 2rem;
		width: 100%;
	}
    &:active &__text {
        color: $LIGHT-GREY;
    }
    &:active &__img {
        fill: $LIGHT-GREY;
    }
    &:focus &__text::before {
        visibility: visible;
    }
   
    &__text {
        text-align: center;
        @extend %flex-row-c;
        align-items: center;
        flex-flow: nowrap;
        text-transform: uppercase;
        font-family: $base-font;
        font-size: 0.625rem;
        line-height: 1;
        font-weight: 700;
        letter-spacing: 0.7px;
        color: $TEXT-COLOR;
        white-space: nowrap;
        @media (max-width: 600px) {
            font-size: 0.9rem;
            font-weight: 600;
		}
        &::before {
            position: absolute;
            content: '';
            background-color: transparent;
            left: -2px;
            right: -2px;
            top: -2px;
            bottom: -2px;
            border: 1px solid $GREY-BORDER-COLOR;
            border-radius: 4px;
            transition: border ease-in-out 0.2s;
            z-index: 0;
            visibility: hidden;
        }
    }
    &__img {
        stroke: none;
        height: 14px;
        width: 16px;
        fill: $TEXT-COLOR;
        margin-left: 10px;
        @media (max-width: 600px) {
            height: 18px;
            width: 18px;
		}
    }
}
</style>
