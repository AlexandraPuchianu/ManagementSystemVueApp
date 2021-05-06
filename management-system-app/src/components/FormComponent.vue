<template>
    <form id="form" onsubmit="return false">
        <label>First name: </label>
        <input type="text" id="fname" placeholder="First name"><br><br>
        <label>Last name: </label>
        <input type="text" id="lname" placeholder="Last Name"><br><br>
        <label>Email: </label>
        <input type="text" id="email" placeholder="Email"><br><br>
        <label>Gender:</label>
        <select id="gender">
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
        </select><br><br>
        <label>Birthdate: </label>
        <input type="date" id="birthdate" value="2003-01-01" min="1921-01-01" max="2021-04-23"><br><br>
        <label>Picture:</label>
        <input type="file" id="picture" onchange="upload(this)"><br><br>
        <button type="submit" class="submitButton" onclick="addEmployee()">Submit</button>
    </form>
</template>

<script>
export default {
    name: 'FormComponent',
}
</script>

<style scoped>
form{
    margin-top: 3rem;
    margin-left: 3rem;
}

.submitButton{
    background-color: #1a73e8;
    border: none;
    color: white;
    margin-left: 1.5rem;
    text-decoration: none;
    font-size: 14px;
    cursor: pointer;
    height: 2.3rem;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    border-radius: 4px;
}
</style>