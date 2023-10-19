<template>
    <div class="modal" @click="closeModal">
        <div class="modal__block" @click.stop="">
            <h2 class="modal__block-title">{{ !edit ? $t('addNote') : $t('changeNote') }} </h2>
            <div class="modal__block-inputs">
                <label>
                    <span>Title</span>
                    <input type="text" v-model="title">
                </label>
                <label>
                    <span>Content</span>
                    <input type="text" v-model="text">
                </label>
            </div>
            <div class="modal__block-btns">
                <button class="modal__block-btns-btn del" @click="closeModal">{{$t('cansel')}}</button>
                <button class="modal__block-btns-btn edit" @click="addNote" v-if="!edit">{{$t('add')}}</button>
                <button class="modal__block-btns-btn edit" @click="changedNote" v-else>{{$t('change')}}</button>
            </div>
        </div>
    </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid'
export default {
    props: {
        editedNote: Object,
        edit: Boolean
    },
    data() {
        return {
            title: '',
            text: ''
        }
    },
    methods: {
        closeModal() {
            this.$emit('close')
            this.text = this.title = ''
        },
        addNote() {
            if (this.title != '' && this.text != '') {
                const note = {
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleDateString(),
                    id: uuidv4()
                }
                this.$emit('addNote', note)
                this.closeModal()
            }

        },
        changedNote() {
            if (this.title != '' && this.text != '') {
                const newEditedNote = {
                    title: this.title,
                    text: this.text,
                    date: new Date().toLocaleDateString(),
                    id: this.editedNote.id
                }
                this.$emit('changedNote', newEditedNote)
                this.closeModal()
            }
        }
    },
}
</script>
