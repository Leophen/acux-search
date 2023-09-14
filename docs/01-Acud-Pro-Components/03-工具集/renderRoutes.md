---
title: renderRoutes
---

根据配置进行的路由渲染，其基于 react-router-dom。

## 引入

```js
import {renderRoutes} from '@baidu/acud-pro-components';
```

## 基本用法

```js
import {Route, Switch, withRouter} from 'react-router-dom';
import {Loading, renderRoutes} from '@baidu/acud-pro-components';
import loadable from 'react-loadable';

const routes = [
    {
        path: '/',
        exact: true,
        component: loadable({
            loader: () =>
                import(/* webpackChunkName: 'demo-list' */ /* webpackMode: "lazy" */ './List'),
            loading: Loading
        })
    },
    {
        path: '/home/demo/form',
        component: loadable({
            loader: () =>
                import(/* webpackChunkName: 'demo-form' */ /* webpackMode: "lazy" */ './Form'),
            loading: Loading
        })
    }
];

const App = props => (
    <Switch>
        {renderRoutes(routes)}
        <Route key="notFound" component={NoMatch} />
    </Switch>
);

export default withRouter(App);
```
