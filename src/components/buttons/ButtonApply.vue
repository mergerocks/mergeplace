<template>
<button class="button-apply" form='book-form'>
	<p class="button-apply__text">
	{{ $t('buttons.apply') }}
	</p> 
</button>
</template>

<script>

export default {
  name: 'ButtonApply'
}
</script>

<style lang="scss">

.button-apply {
	padding: 1rem 2rem;
	background-color: $MERGE-SECONDARY-COLOR;
	border-radius: 3px;
	outline: none;
	border: none;
	text-align: center;
	@extend %flex-row-c;
    align-items: center;
	position: relative;
	z-index: 2;
	transition: background-color ease-in-out 0.1s; 
	&:active {
        background-color: $MERGE-DARK-COLOR;
    }
    &:focus &__text::before {
        visibility: visible;
    }
	&:disabled {
		background-color: $BLACK;
	}
	&:disabled &__text {
		color: $MIDDLE-GREY;
	}
	&__text {
		font-family: $base-font;
		font-size: 0.625rem;
		font-weight: 700;
		line-height: 1.5;
		letter-spacing: 0.7px;
		color: $MAIN-DARK-COLOR;
		text-transform: uppercase;
		transition: color ease-in-out 0.1s; 
		@media (max-width: 600px) {
			font-size: 10pt;
		}
		&::before {
            position: absolute;
            content: '';
            background-color: transparent;
            left: -2px;
            right: -2px;
            top: -2px;
            bottom: -2px;
            border: 1px solid $MERGE-SECONDARY-COLOR;
            border-radius: 4px;
            transition: border ease-in-out 0.2s;
            z-index: 0;
            visibility: hidden;
        }
	}
	
	
}


</style>
