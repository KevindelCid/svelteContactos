<script>
	let personas = [];
	let datosPersonas = {
		id: null,
		name: "",
		email: "",
		telefono: null,
	};
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
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label"
								>Correo Electronico</label
							>
							<input
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Telefono</label>
							<input
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<button type="button" class="btn btn-primary"
							>Agregar Contacto</button
						>
						<button type="button" class="btn btn-primary"
							>Actualizar</button
						>
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
