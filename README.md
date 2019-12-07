# laravel-payment-help-link
paypal

client and server

https://www.youtube.com/watch?v=ESaRZz5V9OI&list=PLe30vg_FG4OSdVn4zFpXNpBILtijJ2-x7&index=4 : paypal tutorial

*: composer require paypal/rest-api-sdk-php

sandbox create your busniss and personal account.

for example: 

paypal.Buttons({
    style: {
        shape: 'pill',
        color: 'blue',
        layout: 'vertical',
        label: 'paypal',
    },
    createOrder: function(data, actions) {
        return actions.order.create({
            purchase_units: [{
                amount: {
                    value: '4'
                }
            }]
        });
    },
    onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
            var url = window.location.href;
            var emailaddress = localStorage.getItem("emailaddress");
            var material = localStorage.getItem("material");
            material = material.split(',');
            var locale = $('html').attr('lang');
            var cal = localStorage.getItem("cal");
            profile = localStorage.getItem("profile");
            profile = profile.split(',');
            $.ajax({
                url: "/savedietplan",
                method: 'post',
                data: {
                    _token: $('meta[name="csrf-token"]').attr("content"),
                    cal: cal,
                    material: material,
                    profile: profile,
                    locale: locale,
                    link: url,
                    email: emailaddress
                },
                success: function (response) {
                    alert("success! Please check your email.");
                    console.log(response);
                }
            })
        });
    }
}).render('#paypal-button-container');
