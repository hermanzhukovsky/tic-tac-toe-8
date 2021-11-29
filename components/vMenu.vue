<template>
	<div class="header__menu menu">
		<button class="menu__icon" :class="{ _active: isActive }" type="button" @click="toggleBurger">
			<span></span>
			<span></span>
			<span></span>
		</button>
		<div class="menu__body" :class="{ _active: isActive }">
			<ul class="menu__list">
				<li class="menu__item"><a class="menu__link fas fa-user-friends" @click.prevent="setMode('multiplayer'), toggleBurger()" href=""><span>Start new game with another player</span></a></li>
				<li class="menu__item"><a class="menu__link fas fa-robot" @click.prevent="setMode('single-player'), toggleBurger()" href=""><span>Start new game with bot</span></a></li>
				<li class="menu__item"><a class="menu__link fas fa-spinner" @click.prevent="loadPreviousGame(), toggleBurger()" href=""><span>Load game</span></a></li>
			</ul>
		</div>
	</div>
</template>

<script>
import { mapMutations } from 'vuex';

export default {

	name: "vMenu",
	data() {
		return {
			isActive: false
		}
	},
	methods: {
		...mapMutations([
			'loadPreviousGame',
			'setMode'
		]),
		toggleBurger() {
			this.isActive = !this.isActive;
		},
	}
}
</script>
<style lang="scss">
.menu {
	display: flex;
	align-items: center;

	&__container {
	}
	&__icon {
		display: block;
      position: relative;
      width: 35px;
      height: 20px;
      cursor: pointer;
      z-index: 3;

      span {
         transition: all 0.3s ease 0s;
         position: absolute;
         left: 0px;
         top: calc(50% - 1px);
         width: 100%;
         height: 2px;
         background-color: #fff;
      }
      span:first-child {
         top: 0px;
      }
      span:last-child {
         top: auto;
         bottom: 0px;
      }
      &._active {
         span {
            transform: scale(0);
				background-color: #fff;
            &:first-child {
               transform: rotate(-45deg);
               top: calc(50% - 1px);
            }
            &:last-child {
               transform: rotate(45deg);
               bottom: calc(50% - 1px);
            }
         }
      }
	}
	&__body {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		opacity: 0;
		visibility: hidden;
		transition: all 0.3s ease 0s;
		overflow: auto;
		align-items: center;
		background-color: #1d1b1b;
		padding: 90px 15px 20px 15px;
		display: flex;
		justify-content: center;
		height: 100%;
		&._active {
			opacity: 1;
			visibility: visible;
		}
		&::before {
			content: '';
			position: fixed;
			z-index: 2;
			top: 0;
			left: 0;
			width: 100%;
			height: 70px;
			background-color: #313131;
		}
	}
	&__list {
		max-width: 1000px;
	}
	
	&__item {
		&:not(:last-child) {
			margin: 0px 0px 34px 0px;
		}
	}
	
	&__link {
		font-size: 24px;
		letter-spacing: 0.045em;
		font-weight: 700;
		color: inherit;
		display: inline-flex;
		align-items: center;
		line-height: 28 / 24 * 100%;
		&:before {
			margin: 0px 12px 0px 0px;
		}
		@media (any-hover: hover) {
			&:hover {
				color: rgb(113, 241, 63);
			}
		}
	}
}
</style>