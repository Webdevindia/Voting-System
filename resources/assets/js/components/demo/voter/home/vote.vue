<template>
<div class="row col-md-12 ">
	<div class="col-md-4">
		<h4>Vote Information</h4><hr/>
		<ul class="list-group">
			<li class="list-group-item" v-for="position in data.positions">
				<b><label v-if="position.name == 'Amenable'">Extend the TENURE of PACPA OFFICERS</label> <label v-else="position.name != 'Amenable'">{{ position.name }}</label> : </b>{{ getName(position.id) }}

			</li>
			<li class="list-group-item">
				<center>
					<button class="btn btn-success" @click="util.showModal('#vote-modal')">Submit Vote</button>
					<button class="btn btn-default" @click="reset()">Reset</button>
				</center>
			</li>
		</ul>
	</div>

	<div class="col-md-8">
		<!--<h4>PACPA</h4><hr/>-->
		<!--<div class="panel panel-info" v-for="position in data.positions">-->
			<!--<div class="panel-heading">{{ position.name }}</div>-->
			<!--<div class="panel-body table-responsive">-->
				<!--<table class="table table-hover">-->
					<!--<thead>-->
					<!--<tr>-->
						<!--<th></th>-->
						<!--<th width="7%"></th>-->
						<!--<th>Name</th>-->
						<!--<th>Team Name</th>-->
						<!--<th>Unit</th>-->
					<!--</tr>-->
					<!--</thead>-->
					<!--<tbody>-->
					<!--<tr v-for="nominee in data.nominees" v-if="nominee.position_id==position.id" @click="vote(position.id,nominee.id)">-->
						<!--<td><input type="radio" :name="position.id" :id="nominee.id" style="width:2em; height:2em; margin-top:2em;"></td>-->
						<!--<td><img :src="data.storageURL+nominee.image" style="height: 80px; width: 80px" class="thumbnail"/></td>-->
						<!--<td><p style="margin-top:2em;">{{ nominee.name }}</p></td>-->
						<!--<td><p style="margin-top:2em;">{{ getPartylist(nominee.partylist_id) }}</p></td>-->
						<!--<td><p style="margin-top:2em;">{{ nominee.course }}</p></td>-->
					<!--</tr>-->
					<!--</tbody>-->
				<!--</table>-->
			<!--</div>-->
		<!--</div>-->
		<!--<div class="panel panel-info" >-->
			<!--<div class="panel-heading"></div>-->
			<!--<div class="panel-body table-responsive">-->
				<!--<table class="table table-hover">-->
					<!--<thead>-->
					<!--<tr>-->
						<!--<td width="100%" style="font-size: 15px"><b>Are you amenable to the extension of PACPA OFFICERS for another one (1) year?</b></td>-->
					<!--</tr>-->
					<!--</thead>-->
					<!--<tbody>-->
					<!--<tr>-->

						<!--<td width="100%">-->
							<!--<input v-model="amenable" id="no" name="amenable" type="radio" class ="cheker" v-bind:value="'yes'" style="width:1.5em; height:1.5em; margin-top:1.5em;"> <label style="font-size: 20px; font-weight: normal">Yes</label>   &emsp;&emsp;-->
							<!--<input v-model="amenable" id="yes" name="amenable" type="radio" class ="cheker" v-bind:value="'no'" style="width:1.5em; height:1.5em; margin-top:1.5em;"> <label style="font-size: 20px; font-weight: normal">No</label>-->

						<!--</td>-->
					<!--</tr>-->
					<!--</tbody>-->

				<!--</table>-->
			<!--</div>-->
		<!--</div>-->

		<div class="panel panel-info" v-for="position in data.positions" v-if="position.name == 'Amenable'">
			<div class="panel-heading"><label v-if="position.name == 'Amenable'">Extend the TENURE of PACPA OFFICERS</label> <label v-else="position.name != 'Amenable'">{{ position.name }}</label></div>
			<div class="panel-body table-responsive">
				<table class="table table-hover">
					<thead>
					<tr>
						<th colspan="3"> Do you agree to EXTEND THE TENURE OF INCUMBENT PACPA OFFICERS for another one (1) year? </th>
						<!--<th width="7%"></th>-->
						<!--<th>Name</th>-->
						<!--<th>Team Name</th>-->
						<!--<th>Unit</th>-->
					</tr>
					</thead>
					<tbody>

					<tr v-for="nominee in data.nominees" v-if="nominee.position_id==position.id" @click="vote(position.id,nominee.id)">
						<td width="5%"><input type="radio" :name="position.id" :id="nominee.id" style="width:2em; height:2em; margin-top:2em;"></td>
						<!--<td><img :src="data.storageURL+nominee.image" style="height: 80px; width: 80px" class="thumbnail"/></td>-->
						<td colspan="2"><p style="margin-top:2em;">{{ nominee.name }}</p></td>

						<!--<td><p style="margin-top:2em;">{{ getPartylist(nominee.partylist_id) }}</p></td>-->
						<!--<td><p style="margin-top:2em;">{{ nominee.course }}</p></td>-->
					</tr>
					</tbody>
				</table>
			</div>
		</div>

		<h4>Select Candidates</h4><hr/>
		<div class="panel panel-info" v-for="position in data.positions" v-if="position.name != 'Amenable'">
			<div class="panel-heading">{{ position.name }}</div>
			<div class="panel-body table-responsive">
				<table class="table table-hover">
					<thead>
						<tr>
							<th></th>
							<th width="7%"></th>
							<th>Name</th>
							<!--<th>Team Name</th>-->
							<th>Unit</th>
						</tr>
					</thead>
					<tbody>

						<tr v-for="nominee in data.nominees" v-if="nominee.position_id==position.id" @click="vote(position.id,nominee.id)">
							<td><input type="radio" :name="position.id" :id="nominee.id" style="width:2em; height:2em; margin-top:2em;"></td>
							<td><img :src="data.storageURL+nominee.image" style="height: 80px; width: 80px" class="thumbnail"/></td>
							<td><p style="margin-top:2em;">{{ nominee.name }}</p></td>
							<!--<td><p style="margin-top:2em;">{{ getPartylist(nominee.partylist_id) }}</p></td>-->
							<td><p style="margin-top:2em;">{{ nominee.course }}</p></td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>
	</div>

	<modal id="vote-modal">
		<modal-header>Vote</modal-header>
		<modal-body>
			<h3>Note: You can only vote once, so vote wisely.</h3>
		</modal-body>
		<modal-footer>
			<button class="btn btn-success" @click="submit()">Submit Vote</button>
			<button class="btn btn-default" data-dismiss="modal">Cancel</button>
		</modal-footer>
	</modal>

</div>

</template>

<script>



export default{
	created: function () {
		if (this.data.result.length > 0 || this.data.election.status != 2) 
			this.$router.push({name: 'Voter Home'})
		for (var i in this.data.positions) {
			this.selected.push({
				position_id: this.data.positions[i]['id'], 
				nominee_id: null, 
			});
		}
	},

	data: function () {
		return {
			selected: [],
			name: {}
		}
	},

	methods: {

		submit: function () {
			this.util.hideModal('#vote-modal');
			if (this.hasNullVote()) return;
			var vm = this;
			this.util.notify('Submitting your vote, please wait...', 'loading');
			let data = {};
			data['vote'] = this.selected;
			axios.post(config.API+'election/vote', data)
				.then(response=>{
					$.notifyClose();
					if (vm.util.showResult(response, 'success')){
						vm.data.result = response.data.result;
						vm.$router.push({name: 'Result'});
					}

				})
				.catch(error=>{
					$.notifyClose();
					vm.util.showResult(error, 'error');
				})

		},

		hasNullVote: function () {
			let selected = this.selected;
			for (var i in selected) 
				if (selected[i]['nominee_id'] == null){
					this.util.notify('You must vote for all positions', 'error');
					return true;
				}
			return false;
		},

		reset: function () {
			let selected = this.selected;
			for (var i in selected){
				$('#'+selected[i]['nominee_id']).selected(false);
				selected[i]['nominee_id'] = null;
			}
		},

		vote: function (position_id, nominee_id) {
			$('#'+nominee_id).selected();
			for (var i in this.selected)
				if (this.selected[i]['position_id'] == position_id) {
					this.selected[i]['nominee_id'] = nominee_id;
				}
		},

		getName: function (id) {
			let positions = this.data.positions;
			let selected = this.selected;
			for (var i in selected) 
				if (selected[i]['position_id'] == id) 
					return this.getNominee(selected[i]['nominee_id']);
			return '';
		},
		getAmenable: function (id) {
			let amenables = this.data.positions;
			let selected = this.selected;
			for (var i in selected)
				if (selected[i]['position_id'] == id)
					return this.getNominee(selected[i]['nominee_id']);
			return '';
		},


		getNominee: function (id) {
			let nominees = this.data.nominees;
			for (var i in nominees)
				if (nominees[i]['id'] == id) return nominees[i]['name'];
		},

		getPartylist: function (id) {
			let partylists = this.data.partylists;
			for (var i in partylists)
				if (partylists[i]['id']==id) return partylists[i]['name'];
			return 'No Team';
		}
	}

}

</script>
