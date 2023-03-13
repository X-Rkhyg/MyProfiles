(function($) {

	"use strict";

	// Init Metronal
	var metronal = {};

	// Init Main Content
	metronal.mainContent = {
		list: ["#home", "#about", "#resume", "#portfolio", "#contact"],
		on: "",
		off: ""
	};

	// Pre Load
	metronal.preLoad = function(duration) {
		$('#pre-load').fadeOut(parseInt(duration, 10));
	};

	// Replace Viewport Height
	// Solves the issue about the viewport height on mobile devices as when the page loads
	metronal.replaceVHeight = function() {
		$('html').css({
			'height': $(window).height()
		});
	};

	// Portfolio Filter
	metronal.portfolioFilter = {
		// Item container
		container: $('#portfolio .portfolio-item .item-wrapper'),
		// Init function
		init: function() {
			// Checking if all images are loaded
			metronal.portfolioFilter.container.imagesLoaded(function() {
				// Init isotope once all images are loaded
	            metronal.portfolioFilter.container.isotope({
	                itemSelector: '#portfolio .portfolio-item .item-wrapper .item',
	                layoutMode: 'masonry',
	                transitionDuration: '0.8s'
	            });
	            // Forcing a perfect masonry layout after initial load
	            metronal.portfolioFilter.container.isotope('layout');
	            // Filter items when the button is clicked
	            $('#portfolio .portfolio-filter ul li').on('click', 'a', function () {
	            	// Remove the current class from the previous element
	                $('#portfolio .portfolio-filter ul li .current').removeClass('current');
	                // Add the current class to the button clicked
	                $(this).addClass('current');
	                // Data filter
	                var selector = $(this).attr('data-filter');
	                metronal.portfolioFilter.container.isotope({
	                    filter: selector
	                });
	                setTimeout(function () {
	                    metronal.portfolioFilter.container.isotope('layout');
	                }, 6);
	                return false;
	            });
	        });
	    } 
	};

	// Use Magnific Popup
	metronal.useMagnificPopup = function() {
		// For portfolio item
		$('#portfolio .portfolio-item .item-wrapper .item').magnificPopup({
			delegate: 'a',
			type: 'inline',
			removalDelay: 300,
			mainClass: 'mfp-fade',
			fixedContentPos: true,
		    callbacks: {
		    	beforeOpen: function() { 
		    		$('html').addClass('mfp-helper'); 
		    	},
		    	close: function() { 
		    		$('html').removeClass('mfp-helper'); 
		    	}
		  	}
		});
	};

	// Set Skill Progress
	metronal.setSkillProgress = function() {
		// Select skill
		var skill = $('.single-skill');
		for(var i = 0; i < skill.length; i++) {
			if(skill.eq(i).find('.percentage')[0].textContent == '100%') {
				skill
					.eq(i)
					.find('.progress-wrapper .progress')
					.css({
						'width': skill.eq(i).find('.percentage')[0].textContent,
						'borderRight': 0
					});
			} else {
				skill
					.eq(i)
					.find('.progress-wrapper .progress')
					.css('width', skill.eq(i).find('.percentage')[0].textContent);
			}
		}
	};

	// Use TypeIt.js
	metronal.useTypeIt = function() {
		if(typeof TypeIt != 'undefined') {
			new TypeIt('.passion', {
				speed: 200,
		        startDelay: 800,
		        strings: ['Nub Developer', 'Loli Hunter', 'Loli Protector', 'CopyPaster'],
		        breakLines: false,
		        loop: true
			}).go();
			
		} else {
			return false;
		}
	};

	// Progress Animation
	metronal.progressAnimation = function() {
		// Disable progress animation on IE Browser
		if(navigator.userAgent.indexOf('MSIE')!==-1 || navigator.appVersion.indexOf('Trident/') > -1) {
			$('.progress-wrapper .progress').css({
				'animation': 'none'
			});
		}
	};

	// Dynamic Page
	metronal.dynamicPage = function(event, target) {
		if(!event) {
			if(!target) {
				$('#home').addClass('active');
				metronal.mainContent.on = metronal.mainContent.off = "#home";
			} else {
				if(metronal.mainContent.list.includes(target)) {
					$(target).addClass('active');
					metronal.mainContent.on = metronal.mainContent.off = target;
				} else {
					$('#home').addClass('active');
					metronal.mainContent.on = metronal.mainContent.off = "#home";
				}
			}
		} else {
			var currentTarget = event.currentTarget;
			var prevMainContentOff = metronal.mainContent.off, 
				targetOff = metronal.mainContent.on,
				targetOn;
			if(currentTarget.className === "menu-link" || currentTarget.className === "close-menu-link" || currentTarget.id === "contact-button") {
				if(metronal.mainContent.list.includes(target)) {
					targetOn = target;
				} else {
					return;
				}
			} else {
				return;
			}


			if(targetOn !== targetOff) {
				$(prevMainContentOff).removeClass("scaleDownCenter");
				$(targetOff).removeClass("scaleDownCenter");
				$(targetOff).removeClass("scaleUpCenter active");
				$(targetOff).addClass("scaleDownCenter");
				$(targetOn).addClass("scaleUpCenter active");

				metronal.mainContent.off = targetOff;
				metronal.mainContent.on = targetOn;
			}
		}
	};

	// Process Contact Form
	metronal.processContactForm = function() {
		var form = $('form[name="contact"]'),
			message = $('.contact-msg'),
			formData;

		// Success Function
		var doneFunc = function(response) {
			message.text(response);
			message
				.removeClass('alert-danger')
				.addClass('alert-success')
				.fadeIn();
			setTimeout(function() {
				message.fadeOut();
			}, 2400);
			form.find('input:not([type="submit"]), textarea').val('');
		};

		// Fail Function
		var failFunc = function(jqXHR, textStatus, errorThrown) {
			if(jqXHR.status === 400) {
				message.text(jqXHR.responseText);
			} else {
				message.text(jqXHR.statusText);
			}
			message
				.removeClass('alert-success')
				.addClass('alert-danger')
				.fadeIn();
			setTimeout(function() {
				message.fadeOut();
			}, 2400);
		};

		// Form On Submit 
		form.on('submit', function(e) {
			e.preventDefault();
			formData = $(this).serialize();
			$.ajax({
				type: 'POST',
				url: form.attr('action'),
				data: formData
			})
			.done(doneFunc)
			.fail(failFunc);
		});
	};

	// Window On Resize
	$(window).on('resize', function() {
		metronal.replaceVHeight(),
		metronal.portfolioFilter.container.isotope('layout');
	});

	// Device Orientation Changes
	window.addEventListener("orientationchange", function () {
		metronal.replaceVHeight(),
        metronal.portfolioFilter.container.isotope('layout');
    }, false);

    // Menu Link On Click
	$(".menu-link").on("click", function(e) {
		metronal.dynamicPage(e, $(this)[0].hash);
	});

	// Close Menu Link On Click
	$(".close-menu-link").on("click", function(e) {
		metronal.dynamicPage(e, $(this)[0].hash);
	});

	// Contact Button On Click
	$("#contact-button").on("click", function(e) {
		metronal.dynamicPage(e, $(this)[0].hash);
	});

	// Prevent Default 'a[href=""]' click
	$('a[href="#"]').on('click', function (e) {
        e.preventDefault();
    });

	// Window On Load
	$(window).on('load', function() {
		metronal.preLoad(800);
	});

	// Document Ready
	$(document).ready(function() {
		metronal.dynamicPage(undefined, window.location.hash),
		metronal.replaceVHeight(),
		metronal.portfolioFilter.init(),
		metronal.useMagnificPopup(),
		metronal.setSkillProgress(),
		metronal.progressAnimation(),
		metronal.useTypeIt(),
		metronal.processContactForm();
	});

})(jQuery);