<script>
	import Nav from '$lib/Nav/Nav.svelte';
	import { open } from '$lib/Nav/stores.js';
</script>

<Nav />
<main class="stack" data-state={$open ? 'nav-expanded' : 'nav-collapsed'}>
	<h1>Occultum facinus esse potuerit, gaudebit;</h1>
	<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. In schola desinis. Mihi, inquam, qui te id ipsum rogavi? Sed in rebus apertissimis nimium longi sumus. Hic ambiguo ludimur. Quid ad utilitatem tantae pecuniae? Age sane, inquam. </p>
	<p>Sed quid sentiat, non videtis. Inde igitur, inquit, ordiendum est. Illum mallem levares, quo optimum atque humanissimum virum, Cn. <a href='http://loripsum.net/' target='_blank' rel='noreferrer'>Quod totum contra est.</a> <b>Quo plebiscito decreta a senatu est consuli quaestio Cn.</b> <i>Cave putes quicquam esse verius.</i> </p>
	<h2>Quod praeceptum quia maius erat, quam ut ab homine videretur, idcirco assignatum est deo.</h2>
	<p>Ita graviter et severe voluptatem secrevit a bono. Quid iudicant sensus? <a href='http://loripsum.net/' target='_blank' rel='noreferrer'>Facillimum id quidem est, inquam.</a> Fortemne possumus dicere eundem illum Torquatum? </p>
	<blockquote cite='http://loripsum.net'>
		Princeps huius civitatis Phalereus Demetrius cum patria pulsus esset iniuria, ad Ptolomaeum se regem Alexandream contulit.
	</blockquote>
	<p><b>Sit enim idem caecus, debilis.</b> Utram tandem linguam nescio? Aliter enim nosmet ipsos nosse non possumus. </p>
	<ul>
		<li>Saepe ab Aristotele, a Theophrasto mirabiliter est laudata per se ipsa rerum scientia;</li>
		<li>Quicquid porro animo cernimus, id omne oritur a sensibus;</li>
		<li>Sed tamen omne, quod de re bona dilucide dicitur, mihi praeclare dici videtur.</li>
		<li>Quod quidem iam fit etiam in Academia.</li>
	</ul>
	<p>Quibus ego vehementer assentior. Pauca mutat vel plura sane; Quid vero? Estne, quaeso, inquam, sitienti in bibendo voluptas? </p>
	<h2>Nondum autem explanatum satis, erat, quid maxime natura vellet.</h2>
	<p>Et quidem, inquit, vehementer errat; Duo Reges: constructio interrete. Maximus dolor, inquit, brevis est. Age, inquies, ista parva sunt. Sed quae tandem ista ratio est? <b>Prioris generis est docilitas, memoria;</b> Nulla erit controversia. </p>
	<p><a href='http://loripsum.net/' target='_blank' rel='noreferrer'>Quae sequuntur igitur?</a> <b>Tum Torquatus: Prorsus, inquit, assentior;</b> Apparet statim, quae sint officia, quae actiones. Apparet statim, quae sint officia, quae actiones. </p>
	<p>Quibus ego vehementer assentior. Prave, nequiter, turpiter cenabat; <a href='http://loripsum.net/' target='_blank' rel='noreferrer'>Honesta oratio, Socratica, Platonis etiam.</a> Refert tamen, quo modo. Haec dicuntur inconstantissime. </p>
</main>

<style>
	main {
		padding: var(--padding);
	}

	@media (max-width: 50rem) {
		main {
			padding-block-start: calc(var(--padding) + var(--nav-button-size) + var(--stack-space));
		}

		main[data-state="nav-expanded"] {
			transform: translateX(var(--nav-width));
		}
	}
</style>
