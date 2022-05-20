<script>
	let personas = [];
	let datoPersona = {
		"name": null,
		"email": "",
		"telefono": null,
	};
	let datosPersonas = {
		id: null,
		name: "",
		email: "",
		telefono: null,
	};

	let mostrarPersonas = () => {
		fetch("http://127.0.0.1:8000/api/auth/sveltelistar")
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				personas = datosRespuesta;
				datosPersonas = {
					id: null,
					name: "",
					email: "",
					telefono: null,
				};
				console.log(personas);
			})
			.catch(console.log);
	};

	let agregarPersona = () => {
		const nuevaPersona = {
			
			"name": datoPersona.name,
			"email": datoPersona.email,
			"telefono": datoPersona.telefono,
		};
		console.log(nuevaPersona);

		fetch("http://127.0.0.1:8000/api/auth/svelteapi", {
			method: "POST",
			headers: {
                // tenemos que avisar que vamos a enviar los datos en formato JSON
                'Content-Type': 'application/json'
            },
			body: JSON.stringify(nuevaPersona),
		})
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				console.log(datosRespuesta);
				mostrarPersonas();
			})
			.catch(console.log);
	};

	mostrarPersonas();
	// []
</script>

<div class="container">
	<div class="row">
		<div class="col-md-5">
			<div class="card">
				<div class="card-header">Personas</div>
				<div class="card-body">
					<form action="">
						<div class="mb-3">
							<label for="" class="form-label">Nombre</label>
							<input
								bind:value={datoPersona.name}
								type="text"
								class="form-control"
								name="name"
								id="name"
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label"
								>Correo Electronico</label
							>
							<input
								bind:value={datoPersona.email}
								type="text"
								class="form-control"
								name="email"
								id="email"
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Telefono</label>
							<input
								bind:value={datoPersona.telefono}
								type="text"
								class="form-control"
								name="telefono"
								id="telefono"
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<button
							type="button"
							class="btn btn-primary"
							on:click|preventDefault={agregarPersona}
							>Agregar Contacto</button
						>
						<!-- <button type="button" class="btn btn-primary"
							>Actualizar</button
						> -->
					</form>
				</div>
			</div>
		</div>

		<div class="col-md-7">
			<table class="table">
				<thead>
					<tr>
						<th>ID</th>
						<th>Nombre</th>
						<th>Correo</th>
						<th>Telefono</th>
						<th>Acciones</th>
					</tr>
				</thead>
				<tbody>
					{#each personas as persona}
						<tr>
							<td>{persona.id_contacto}</td>
							<td>{persona.name}</td>
							<td>{persona.email}</td>
							<td>{persona.telefono} </td>
							<td>
								<button
									type="submit"
									name="editar"
									class="btn btn-warning">Editar</button
								>

								|
								<button
									type="submit"
									name="eliminar"
									class="btn btn-danger">Eliminar</button
								>
							</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</div>
</div>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
