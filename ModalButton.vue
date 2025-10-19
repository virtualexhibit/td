<template>
  <transition name="fade">
    <div v-if="show" class="modal-backdrop" @click.self="close">
      <transition name="slide-up">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">{{ modalData.display.title }}</h5>
            <button type="button" class="btn-close" @click="close">×</button>
          </div>

          <div class="modal-body">
            <ul class="qa-list">
              <li v-for="(item, index) in modalData.display.items" :key="index" class="qa-item">
                <p class="question"><strong>Q:</strong> {{ item.q }}</p>
                <p class="answer"><strong>A:</strong> {{ item.a }}</p>
              </li>
            </ul>
          </div>

          <div class="modal-footer">
            <button class="btn-close-footer" @click="close">Close</button>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>
import { MODAL_RECIPE } from '../Recipes/rModalButton.js'

export default {
  name: 'ModalButton',
  props: {
    item: { type: Object, default: () => ({}) },
    show: Boolean,
  },
  emits: ['close'],
  computed: {
    modalData() {
      return {
        directives: { ...MODAL_RECIPE.directives, ...this.item.directives },
        display: { ...MODAL_RECIPE.display, ...this.item.display },
      }
    },
  },
  methods: {
    close() {
      this.$emit('close')
    },
  },
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.3s ease;
}
.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(30px);
  opacity: 0;
}

.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(17, 17, 17, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1050;
  backdrop-filter: blur(5px);
}

.modal-content {
  background: #fff;
  border-radius: 16px;
  width: 480px;
  max-width: 92%;
  padding: 1.5rem;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
  overflow: hidden;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 0.8rem;
}

.modal-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #333;
  margin: 0;
}

.btn-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  color: #999;
  cursor: pointer;
  transition: color 0.2s ease;
}
.btn-close:hover {
  color: #333;
}

.modal-body {
  margin-top: 1rem;
  max-height: 300px;
  overflow-y: auto;
  padding-right: 0.5rem;
}

.qa-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.qa-item {
  background: #f9fafb;
  border: 1px solid #eee;
  border-radius: 10px;
  padding: 0.8rem 1rem;
  margin-bottom: 0.75rem;
  transition: background 0.3s ease, transform 0.2s ease;
}
.qa-item:hover {
  background: #f0f3f8;
  transform: scale(1.01);
}

.question {
  font-weight: 600;
  color: #2a2a2a;
  margin-bottom: 0.3rem;
}

.answer {
  color: #555;
  font-size: 0.95rem;
  line-height: 1.4;
}

.modal-footer {
  text-align: right;
  margin-top: 1rem;
}

.btn-close-footer {
  background: linear-gradient(90deg, #007bff, #00c6ff);
  color: white;
  border: none;
  padding: 0.45rem 1rem;
  border-radius: 6px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.2s ease;
}
.btn-close-footer:hover {
  background: linear-gradient(90deg, #005fcc, #00a3e0);
  transform: scale(1.05);
}
</style>
