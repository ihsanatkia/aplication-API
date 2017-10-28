Aplication API
===========
Request data from https://swapi.co/api/people with ajax Jquery

<pre>
(function($) {
	var indexPeople = 1;
	var maxPeople	= 87;
	
    $(document).on('ready', function(e) {
		loadData(1);        
	});
	
	function loadData(indexPeople){
		var colors = ["purple", "orange"];
		var indexColors = 0;
		
		$(".skywalker").html("");
		
		$.ajax({
            url: "https://swapi.co/api/people/"+indexPeople,
            type: "GET",
            dataType: "JSON",
            success: function(response){
				$("#height").html( response.height );
				$("#mass").html( response.mass );
				$("#hair_color").html( response.hair_color );
				$("#skin_color").html( response.skin_color );
				$("#birth_year").html( response.birth_year );
				$("#gender").html( response.gender );
				$("#name").html( response.name );
				
				/* Manipulate Film */
				$.each(response.films, function(index, url){
					$.ajax({
						url: url,
						type: "GET",
						dataType: "JSON",
						success: function(responseFilm){
							$(".skywalker").append('<li>'+
									'<div class="video">'+
										'<div class="top '+ colors[indexColors] +'">'+
											'<a href="#"><i class="fa fa-play-circle-o" aria-hidden="true"></i></a>'+
										'</div>'+
										'<h2>'+ responseFilm.title +'</h2>'+
										'<div class="director">'+
										'	<label for="">director</label>'+
										'	<span>'+ responseFilm.director +'</span>'+
										'</div>'+
										'<div class="release">'+
										'	<label for="">release</label>'+
										'	<span>'+ responseFilm.release_date+'</span>'+
										'</div>'+
									'</div>'+
								'</li>'
							);
							
							if( indexColors == 0 ){
								indexColors = 1;
							} else {
								indexColors = 0;
							}
						},
						error: function(jqXHR, errorThrown, textStatus){
							console.log(textStatus);
						}
					});
				});
				console.log(response);
            },
            error: function(jqXHR, errorThrown, textStatus){
                console.log(textStatus);
            }
        });
	}

	$("#btn-next").on('click', function(e){
		indexPeople = indexPeople + 1;
		
		loadData( indexPeople );
	});
	
	$("#btn-prev").on('click', function(e){
		indexPeople = indexPeople - 1;
		
		loadData( indexPeople );
	});
})(jQuery);
</pre>
