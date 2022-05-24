<script>
	import { paginate, DarkPaginationNav } from "svelte-paginate";
	let personas = [];
	$: items = busqueda;
	let currentPage = 1;
	let pageSize = 8;
	$: paginatedItems = paginate({ items, pageSize, currentPage });
	let buscar = "";

	$: busqueda = personas.filter((personita)=>{
		currentPage = 1;
		return  personita.nombre_trabajador.toLowerCase().includes(buscar.toLowerCase()) || personita.dpi.toLowerCase().includes(buscar.toLowerCase())
		|| personita.telefonos.toLowerCase().includes(buscar.toLowerCase())  || personita.esquema_vacunas.toLowerCase().includes(buscar.toLowerCase())
		|| personita.departamento.toLowerCase().includes(buscar.toLowerCase()) || personita.municipio.toLowerCase().includes(buscar.toLowerCase())
		|| personita.aldea_barrio_ref.toLowerCase().includes(buscar.toLowerCase());
	});
	

	let datoPersona = {
		nombre_trabajador: null,
		sexo: null,
		dpi: null,
		departamento: null,
		municipio: null,
		aldea_barrio_ref: null,
		telefonos: null,
		pasaporte_vigente: null,
		esquema_vacunacion: null,
		ingreso: null,
		pago: null,
		estado: null,
		nota: null,
		fecha_ingreso: null,
	};
	let datosPersonas = {
		id: null,
		name: "",
		email: "",
		telefono: null,
	};

	let limpiar = () => {
		datoPersona.nombre_trabajador = "";
		datoPersona.sexo = "";
		datoPersona.dpi = "";
		datoPersona.departamento = "";
		datoPersona.municipio = "";
		datoPersona.aldea_barrio_ref = "";
		datoPersona.telefonos = "";
		datoPersona.pasaporte_vigente = "";
		datoPersona.esquema_vacunas = "";
		datoPersona.ingreso = "";
		datoPersona.pago = "";
		datoPersona.estado = "";
		datoPersona.nota = "";
		datoPersona.fecha_ingreso = "";
	};

	let mostrarPersonas = () => {
		fetch("http://127.0.0.1:8000/api/auth/llslistar")
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				personas = datosRespuesta;
				datosPersonas = {
					id: null,
					name: "",
					email: "",
					telefono: null,
				};
				
			})
			.catch(console.log);
	};

	//continuar con la edicion
	let editarPersona = (persona) => {
		datoPersona = persona;
	};

	let actualizarPersona = () => {
		if(datoPersona.id_worker){
		
		fetch(
			"http://127.0.0.1:8000/api/auth/llseditar/" + datoPersona.id_worker,
			{
				method: "POST",
				//	mode: 'no-cors',

				headers: {
					// tenemos que avisar que vamos a enviar los datos en formato JSON
					"Content-Type": "application/json",
				},
				body: JSON.stringify(datoPersona),
			}
		);
		
		
		alert("El trabajador ha sido actualizado");
		mostrarPersonas();
		limpiar();
		} else{

			alert("Necesitas primero seleccionar un trabajador");
		}
	};

	let agregarPersona = () => {
		const nuevaPersona = {
			nombre_trabajador: datoPersona.nombre_trabajador,
			sexo: datoPersona.sexo,
			dpi: datoPersona.dpi,
			departamento: datoPersona.departamento,
			municipio: datoPersona.municipio,
			aldea_barrio_ref: datoPersona.aldea_barrio_ref,
			telefonos: datoPersona.telefonos,
			pasaporte_vigente: datoPersona.pasaporte_vigente,
			esquema_vacunas: datoPersona.esquema_vacunas,
			ingreso: datoPersona.ingreso,
			pago: datoPersona.pago,
			estado: datoPersona.estado,
			nota: datoPersona.nota,
			fecha_ingreso: datoPersona.fecha_ingreso,
		};

		

		fetch("http://127.0.0.1:8000/api/auth/llsinsert", {
			method: "POST",
			headers: {
				// tenemos que avisar que vamos a enviar los datos en formato JSON
				"Content-Type": "application/json",
			},
			body: JSON.stringify(nuevaPersona),
		})
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				
				mostrarPersonas();
				alert("New Worker inserted in the data base");
				limpiar();
			})
			.catch(console.log);
	};

	mostrarPersonas();

	// []
</script>





<div class="cosa" style="margin-top:50px;">
	<div class="col-md-12">
		<div class="box">
			<!-- <h3 class="heading">How Can We Help?</h3> -->
			<div class="mb-5">
				<div class="row">
					<div class="col-md-5 form-group">
						<!-- ////////////////////////////// -->
<h3>Ingresar o actualizar a una persona </h3>
						<form action="">
							<div class="col-md-12">
								<div class="box">
									<div class="mb-5">
										<div class="row">
											<div class="col-md-12 form-group">
												<label for="" class="form-label"
													>Nombre</label
												>
												<input
													bind:value={datoPersona.nombre_trabajador}
													type="text"
													class="form-control"
													name="name"
													id="name"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-2 form-group">
												<label for="" class="form-label"
													>sexo</label
												>
												<input
													bind:value={datoPersona.sexo}
													type="text"
													class="form-control"
													name="sexo"
													id="sexo"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-10 form-group">
												<label for="" class="form-label"
													>dpi</label
												>
												<input
													bind:value={datoPersona.dpi}
													type="text"
													class="form-control"
													name="dpi"
													id="dpi"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-6 form-group">
												<label for="" class="form-label"
													>Departamento</label
												>
												<input
													bind:value={datoPersona.departamento}
													type="text"
													class="form-control"
													name="departamento"
													id="departamento"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-6 form-group">
												<label for="" class="form-label"
													>Municipio</label
												>
												<input
													bind:value={datoPersona.municipio}
													type="text"
													class="form-control"
													name="municipio"
													id="municipio"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-4 form-group">
												<label for="" class="form-label"
													>Direccion</label
												>
												<input
													bind:value={datoPersona.aldea_barrio_ref}
													type="text"
													class="form-control"
													name="aldea_barrio_ref"
													id="aldea_barrio_ref"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-4 form-group">
												<label for="" class="form-label"
													>telefonos</label
												>
												<input
													bind:value={datoPersona.telefonos}
													type="text"
													class="form-control"
													name="telefonos"
													id="telefonos"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-2 form-group">
												<label for="" class="form-label"
													>Pasaporte vigente?</label
												>
												<input
													bind:value={datoPersona.pasaporte_vigente}
													type="text"
													class="form-control"
													name="pasaporte_vigente"
													id="pasaporte_vigente"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-2 form-group">
												<label for="" class="form-label"
													>Esquema de vacunacion</label
												>
												<input
													bind:value={datoPersona.esquema_vacunas}
													type="text"
													class="form-control"
													name="esquema_vacunas"
													id="esquema_vacunas"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-2 form-group">
												<label for="" class="form-label"
													>ingreso</label
												>
												<input
													bind:value={datoPersona.ingreso}
													type="text"
													class="form-control"
													name="ingreso"
													id="ingreso"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-2 form-group">
												<label for="" class="form-label"
													>pago</label
												>
												<input
													bind:value={datoPersona.pago}
													type="text"
													class="form-control"
													name="pago"
													id="pago"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-4 form-group">
												<label for="" class="form-label"
													>estado</label
												>
												<input
													bind:value={datoPersona.estado}
													type="text"
													class="form-control"
													name="estado"
													id="estado"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>
											<div class="col-md-4 form-group">
												<label for="" class="form-label"
													>fecha de ingreso</label
												>
												<input
													bind:value={datoPersona.fecha_ingreso}
													type="text"
													class="form-control"
													name="fecha_ingreso"
													id="fecha_ingreso"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-8 form-group">
												<label for="" class="form-label"
													>nota</label
												>
												<input
													bind:value={datoPersona.nota}
													type="text"
													class="form-control"
													name="nota"
													id="nota"
													aria-describedby="helpId"
													placeholder=""
												/>
											</div>

											<div class="col-md-7 form-group">
												<button
													type="button"
													class="btn btn-primary form-control"
													on:click|preventDefault={agregarPersona}
													>Add Worker</button
												>
											</div>
											<div class="col-md-4 form-group">
												<button
													type="button"
													class="btn btn-warning form-control"
													on:click|preventDefault={actualizarPersona}
													>Upgrade Worker</button
												>
											</div>
											<div class="col-md-1 form-group">
											
											<button class="btn btn-danger" on:click|preventDefault={limpiar} >X </button>
											</div>
										</div>
									</div>
								</div>
							</div>
						</form>

						<!-- /////////////////// -->
					</div>
					<div class="col-md-7 form-group">
<h3>Buscar Personas</h3>
						<input type="text" class="form-control" name="buscar" id="buscar" placeholder="Buscar..." bind:value={buscar}>


						<table class="table">
							<thead>
								<tr>
									<th>correlativo</th>
									<th>Nombre</th>
									<th>sexo</th>
									<th>dpi</th>
									<th>Acciones</th>
								</tr>
							</thead>
							<tbody>
								{#if busqueda.length}
								{#each paginatedItems as persona}
									<tr>
										<td>{persona.correlativo}</td>
										<td>{persona.nombre_trabajador}</td>
										<td>{persona.sexo}</td>
										<td>{persona.dpi} </td>
										<td>
											<a
												href="http://mexicanlabor.com/workers?federal_id={persona.dpi}&oid=5011661&owid=186117"
												target="_blank">gestionar</a
											>

											|
											<button
												type="submit"
												name="editar"
												class="btn btn-warning"
												on:click|preventDefault={editarPersona(
													persona
												)}>Editar</button
											>
										</td>
									</tr>
								{/each}
								{:else}
								<span>Ninguna personas se identifica con: "{buscar}"</span>
								{/if}
							</tbody>
						</table>
						<DarkPaginationNav
							totalItems={items.length}
							{pageSize}
							{currentPage}
							limit={1}
							showStepOptions={true}
							on:setPage={(e) => (currentPage = e.detail.page)}
						/>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.cosa {
		margin-top: 15px;
	}
</style>
