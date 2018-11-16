<template>
    <div class="container">
        <form>
            <div class="row">
                <div class="col-xs-12 col-md-6 col-sm-8 col-md-offset-3 col-sm-offset-2">
                   <!--==================
                   -------file complaint
                   ======================-->
                    <h1>File Complaint</h1>
                    <hr>
                    <div class="form-group">
                        <label for="email">
                            Mail
                        </label>
                        <input type="text" id="email" class="form-control" :value="userData.email" @input="userData.email = $event.target.value">
                    </div>
                    <div class="form-group">
                        <label for="password">
                            Password
                        </label>
                        <input type="password" id="password" class="form-control" v-model.lazy="userData.password">
                    </div>
                    <div class="form-group">
                        <label for="age">
                            Age
                        </label>
                        <input type="age" id="age" class="form-control" v-model.lazy.number="userData.age">
                    </div>
                </div>
            </div>
            <!--==================
                   -------horizontal line
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-md-offset-3 col-sm-offset-2">
                    <hr>
                </div>
            </div>
            <!--==================
                   -------message
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-md-6 col-sm-8 col-md-offset-3 col-sm-offset-2 form-group">
                    <label for="message">
                        Message
                    </label>
                    <br>
                    <textarea id="message" cols="76" rows="5" class="form-control" v-model.lazy="message"></textarea>
                </div>
            </div>
            <!--==================
                   -------send mail
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-sm-offset-2 col-md-offset-3">
                    <div class="form-group">
                        <label for="sendmail">
                            <input type="checkbox" id="sendmail" value="SendMail" v-model="sendMail">
                            Send Mail
                        </label>
                        <label for="sendInfomail">
                            <input type="checkbox" id="sendInfomail" value="SendInfoMail" v-model="sendMail">
                            Send Info Mail
                        </label>
                    </div>
                </div>
            </div>
            <!--==================
                   -------gender
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-sm-offset-2 col-md-offset-3 form-group">
                    <label for="male">
                        <input type="radio" id="male" value="male" v-model="gender">
                        Male
                    </label>
                    <label for="female">
                        <input type="radio" id="female" value="female" v-model="gender">
                        Female
                    </label>
                    <label for="other">
                        <input type="radio" id="other" value="other" v-model="gender">
                        other
                    </label>
                </div>
            </div>
            <!--==================
                   -------horizontal line
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-md-offset-3 col-sm-offset-2">
                    <hr>
                </div>
            </div>
            <!--==================
                   -------priority
                   ======================-->
            <div class="row">
                <div class="col-sm-8 col-xs-12 col-md-6 col-sm-offset-2 col-md-offset-3 form-group">
                    <label for="priority">
                        Priority
                    </label>
                    <select id="priority" class="form-control" v-model="selectedPriority">
                        <option v-for="prior in priorities">{{ prior }}</option>
                    </select>
                </div>
            </div>
            <!--==================
                   -------horizontal line
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-md-offset-3 col-sm-offset-2">
                    <hr>
                </div>
            </div>
            <!--==================
                   -------button
                   ======================-->
            <div class="row">
                <div class="col-sm-8 col-xs-12 col-md-6 col-sm-offset-2 col-md-offset-3">
                    <app-switch v-model="dataSwitch"></app-switch>
                </div>
            </div>
            <!--==================
                   -------horizontal line
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-md-offset-3 col-sm-offset-2">
                    <hr>
                </div>
            </div>      
            <!--==================
                   -------submit
                   ======================-->
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-md-6 col-sm-offset-2 col-md-offset-3">
                    <button class="btn btn-primary" @click.prevent="submitted">
                        Submit
                    </button>
                </div>
            </div>
        </form>
        <!--==================
                   -------horizontal line
                   ======================-->
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-md-6 col-md-offset-3 col-sm-offset-2">
                <hr>
            </div>
        </div>
        <!--==================
                   -------user data
                   ======================-->
        <div class="row" v-if="isSubmitted">
            <div class="col-xs-12 col-sm-8 col-md-6 col-sm-offset-2 col-md-offset-3">
                <div class="panel panel-default">
                    <div class="panel-heading">
                        <h4>Your Data</h4>
                    </div>
                    <div class="panel-body">
                        <p>Mail: {{ userData.email }}</p>
                        <p>Password: {{ userData.password }}</p>
                        <p>Age: {{ userData.age }}</p>
                        <p style="white-space: pre">Message: {{ message }}</p>
                        <p><strong>Send Mail?</strong></p>
                        <ul>
                            <li v-for="items in sendMail">{{ items }}</li>
                        </ul>
                        <p>Gender: {{ gender }}</p>
                        <p>Priority: {{ selectedPriority }}</p>
                        <p>Switched: {{ dataSwitch }}</p>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
    import Switch from './Switch.vue';
    export default {
        data() {
            return {
                userData: {
                    email: '',
                    password: '',
                    age: ''
                },
                message: '',
                sendMail: [],
                gender: '',
                selectedPriority: 'High',
                priorities: ['High', 'Medium', 'Low'],
                dataSwitch: true,
                isSubmitted: false
            }
        },
        methods: {
            submitted() {
                this.isSubmitted = true;
            }
        },
        components: {
            appSwitch: Switch
        }
    }
</script>

<style>

</style>
