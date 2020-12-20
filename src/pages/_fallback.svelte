<script>
    import {Container, Row, Col} from 'sveltestrap';
    import {route} from '@sveltech/routify';
</script>


<Container>
    <Row>
        <Col>
            <h1 class="text-center">404</h1>
            <p class="text-center">The path <code>{$route.path}</code> was not found  </p>
            <a href="/">Go to Index</a>
        </Col>
    </Row>
</Container>