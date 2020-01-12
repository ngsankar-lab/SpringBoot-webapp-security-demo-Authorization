# SpringBoot-webapp-security-demo-Authorization
Spring Boot webapp security with Authorization implementation

What is it?
----------
Spring Boot Authorization implemented using roles
inMermoryAuthentication

How?
----
Created a class by extending WebSecurityConfigurerAdapter, with the annotation @EnableWebSecurity

Authentication: Override the method configure(AuthenticationManagerBuilder auth)
      auth.inMemoryAuthentication()
          .withUser("one")
          .password("one")
          .roles("USER")
          .and()
          .withUser("two")
          .password("two")
          .roles("ADMIN");
          
Authorization: Override the method configure(HttpSecurity http)

		http.authorizeRequests()
			.antMatchers("/admin").hasRole("ADMIN")
			.antMatchers("/user").hasAnyRole("USER","ADMIN")
			.antMatchers("/").permitAll()
			.and().formLogin();
