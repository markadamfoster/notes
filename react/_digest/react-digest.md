# React Digest

A summary of (some of) my notes on ReactJS

## Render Props

```js
class Mouse extends React.Component {
  static propTypes = {
    render: PropTypes.func.isRequired
  }

  state = { x: 0, y: 0 }

  handleMouseMove = event => {
    this.setState({
      x: event.clientX,
      y: event.clientY
    })
  }

  render() {
    return (
      <div onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    )
  }
}

const App = React.createClass({
  render() {
    return (
      <div>
        <Mouse
          render={({ x, y }) => (
            <h1>
              The mouse position is ({x}, {y})
            </h1>
          )}
        />
      </div>
    )
  }
})
```
